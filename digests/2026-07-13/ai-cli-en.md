# AI CLI Tools Community Digest 2026-07-13

> Generated: 2026-07-13 01:23 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report
**Date: 2026-07-13**

---

## 1. Ecosystem Overview

The AI CLI development tools ecosystem continues to mature rapidly, with seven major open-source projects serving distinct developer workflows. The landscape is characterized by a tension between model provider lock-in (OpenAI Codex, Anthropic Claude Code) and provider-agnostic tools (OpenCode, Pi, DeepSeek TUI, Gemini CLI). Across all tools, three systemic challenges dominate: **false-positive safety classifiers interrupting legitimate workflows**, **multi-agent orchestration reliability**, and **Windows platform stability gaps**. The ecosystem is seeing a shift from single-session chat interfaces toward persistent daemon architectures, cross-session agent memory, and structured output reliability—indicating that developers are increasingly using AI CLI tools for production, long-running tasks, not just one-off code generation.

---

## 2. Activity Comparison

| Tool | Open Issues | PRs (24h) | New Releases | Community Engagement Signal |
|------|------------|-----------|--------------|---------------------------|
| **Claude Code** | 10+ hot issues | 3 PRs | None | Highest 👍 counts (38–28 per issue); broadest issue diversity |
| **OpenAI Codex** | 10 hot issues | 3 PRs | None | 121 👍 on single issue (#31814); strong agent-model debate |
| **Gemini CLI** | 10 hot issues | 10 PRs | None | Heavy PR activity; critical CVE fixes (Vitest, shell-quote) |
| **GitHub Copilot CLI** | 10 hot issues | 1 PR | None | 8 👍 on TUI wedge; stability-focused |
| **OpenCode** | 10 hot issues | 10 PRs | None | 105 👍 on clipboard bug; broad provider support challenges |
| **Pi (mono)** | 10+ hot issues | 10 PRs | None | Fastest issue-to-close cycle; TUI v2 features |
| **Qwen Code** | 10 hot issues | 12 PRs | None | Highest PR throughput; daemon architecture focus |
| **DeepSeek TUI** | 10 issues | 10 PRs | None | 752-key Korean locale merged; provider expansion |
| **Kimi Code CLI** | 3 hot issues | 2 PRs | None | Lowest activity; Windows compatibility focus |

**Key observations:**
- **Qwen Code** leads in PR throughput (12 PRs), followed by **Gemini CLI** and **OpenCode** (10 each).
- **Claude Code** and **OpenAI Codex** have the highest community engagement per issue (👍 counts), reflecting their larger user bases.
- **Kimi Code CLI** has the lowest activity, indicating a smaller or less vocal community.
- **No tool released a new version today**—all are in development cycles without patches.

---

## 3. Shared Feature Directions

### 3.1 Multi-Agent & Subagent Orchestration (All tools)
- **Claude Code**: Advisor tool failures at high token counts (#67609), cowork sandbox regressions
- **OpenAI Codex**: GPT-5.6 Sol forces MultiAgent V2, hides subagent controls (#31814)—most upvoted issue ecosystem-wide
- **Gemini CLI**: Subagents report false "GOAL" success (#22323); generalist hangs (#21409)
- **GitHub Copilot CLI**: `write_agent` blocks until target wakes (#4101); multi-agent coordination gaps
- **OpenCode**: Agent loops in KIMI K2, MiniMax models (#3743)
- **Pi**: AgentSession lifecycle meta-issue (#5886); post-run continuation bugs
- **Qwen Code**: Background agents for cross-session persistence (#6755); tool-call lifecycle events
- **DeepSeek TUI**: Tool-use block ordering failures (#4329)

**Trend**: Every tool is struggling with reliable subagent delegation, false completion signals, and user-configurable agent hierarchies. The ecosystem lacks a standard pattern for agent lifecycle management.

### 3.2 Windows Platform Parity (All tools with Windows support)
- **Claude Code**: Cowork sandbox crashes (#76094), click-through permission vulnerability (#76743), no RTL text (#75196)
- **OpenAI Codex**: App freezes (#20214), sandbox stuck (#32492), Chrome detection broken (#25271), Norton false-positive malware (#32331)
- **Gemini CLI**: Terminal corruption on resize (#28370)
- **GitHub Copilot CLI**: TUI wedge in WSL2 (#4069), file-locking plugin updates (#4095)
- **OpenCode**: General Windows compatibility (though fewer specific reports this cycle)
- **DeepSeek TUI**: BSD platform builds fixed (#4349); Windows-specific issues less prominent
- **Kimi Code CLI**: UnicodeDecodeError (#2313), missing binary version info (#2178)

**Trend**: Windows remains the "second-class citizen" across all tools. File locking, terminal corruption, sandbox crashes, and encoding errors indicate insufficient cross-platform testing. **Gemini CLI** and **DeepSeek TUI** appear least affected—likely due to Rust/TUI-native architectures.

### 3.3 False-Positive Safety Classifiers (Claude Code, OpenAI Codex)
- **Claude Code**: Pet food analysis triggers model downgrade (#77006); cybersecurity false positives blocking Minecraft modding (#65891), git push, arithmetic
- **OpenAI Codex**: GPT-5.6 Sol false-positive on routine code (#32095); Norton flags Codex as malware (#32331)
- **Gemini CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI, Kimi Code CLI**: No similar reports this cycle

**Trend**: Safety over-alerting is concentrated in the two largest proprietary-model tools. The open-source/provider-agnostic tools appear immune, likely because they lack proprietary safety classifiers or have more conservative guardrails.

### 3.4 Structured Output Reliability (Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI)
- **Claude Code**: Headless JSON Schema serializes arrays as XML (#77026)
- **OpenAI Codex**: GitHub MCP plugin malformed JSON-RPC (#64654)
- **Gemini CLI**: Tool configuration fragility (MCP wildcard deny blocking all tools, #28365 fix)
- **GitHub Copilot CLI**: Session resume corrupts events.jsonl (#4098); binary diffs exceed 5MB limit (#4097)
- **DeepSeek TUI**: Tool schema `oneOf`/`anyOf`/`allOf` causes Anthropic HTTP 400 (#4346)

**Trend**: Structured output—whether JSON schema, MCP tool results, or session persistence—remains fragile across the board. The ecosystem needs standardized tool-call formatting and validation layers.

### 3.5 Cross-Session Persistence & Memory (Qwen Code, Pi, Gemini CLI, OpenCode)
- **Qwen Code**: Devlog + Living Spec background agents (#6755); per-session overhead tracking (#6312)
- **Pi**: AgentSession lifecycle meta-issue (#5886); full-history pager merged (#6580)
- **Gemini CLI**: Auto Memory retries low-signal sessions indefinitely (#26522); token leak before redaction (#26525)
- **OpenCode**: SQLite database bloat to 13GB+ (#33356); no automatic compaction
- **Claude Code**: No explicit memory/persistence features this cycle

**Trend**: The community is moving from "stateless chat" to "persistent AI coworker." Tools that invest in robust session management, automatic memory, and cross-session context will differentiate themselves.

### 3.6 MCP/Plugin Ecosystem Integration (All tools)
- **Claude Code**: GitHub MCP plugin broken (#64654); plugin ecosystem growing
- **OpenAI Codex**: MCP tool call crashes entire app (#32653); OAuth token bridging fails (#4096)
- **Gemini CLI**: MCP tools blocked by wildcard deny (#28365 fix)
- **GitHub Copilot CLI**: Plugin marketplace Git credential failures (#4103); Windows file-locking (#4095)
- **OpenCode**: MCP server dialogs show empty lists (#36580); plugin loading broken (#36525)
- **Pi**: Extension API maturity requests; session replacement API
- **Qwen Code**: Extension management v2 PR (#6638); per-workspace activation
- **DeepSeek TUI**: Provider expansion (MiniMax, custom routes); schema normalization

**Trend**: MCP and plugin architectures are becoming the standard extension mechanism, but every tool has integration bugs—especially around authentication, credential bridging, and trust models.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI | Kimi Code |
|-----------|-------------|--------------|------------|-------------|----------|-----|------------|--------------|-----------|
| **Model Focus** | Proprietary (Claude) | Proprietary (GPT) | Proprietary (Gemini) | Multi-model | Multi-provider | Multi-provider | Multi-provider (Qwen focus) | Multi-provider | Proprietary (Kimi) |
| **Architecture** | Monolithic CLI + VS Code ext | Desktop app + CLI | CLI + background daemon | CLI + VS Code ext | Desktop app + CLI | TUI-first | CLI + `qwen serve` daemon | TUI-first | Python-based CLI |
| **Key Differentiator** | Advisor tool, permissions model | Agent hierarchy, MultiAgent V2 | Subagent delegation, AST tools | GitHub integration, voice mode | Provider flexibility, v2 architecture | TUI polish, fast iteration | Multi-workspace daemon, skill system | Provider-agnostic, BSD support | Minimalist, Windows focus |
| **Primary Pain Point** | Safety false positives | Agent model override | Subagent reliability | Terminal stability | SQLite bloat, provider bugs | Agent lifecycle | CI instability, streaming | Anthropic schema issues | Rate limit confusion |
| **Community Size (est.)** | Largest | Largest | Medium | Medium-Large | Medium | Medium-Small | Medium | Small | Smallest |
| **Iteration Speed** | Medium | Slow | High | Medium | High | High | Highest | High | Slow |

### Key Strategic Differences:

**1. Architecture Philosophy:**
- **Daemon-centric**: Qwen Code, Gemini CLI, OpenCode (v2) are moving toward long-running daemon processes with multi-workspace support.
- **Session-based**: Claude Code, OpenAI Codex, Copilot CLI remain session-oriented, with less cross-session persistence.
- **TUI-native**: Pi and DeepSeek TUI prioritize terminal-native UX with fast rendering, minimal dependencies.

**2. Provider Lock-in vs. Agnosticism:**
- **Lock-in**: Claude Code (Anthropic), OpenAI Codex (OpenAI), Kimi Code (Moonshot) are tied to their parent company's models.
- **Agnostic**: OpenCode, Pi, Qwen Code, DeepSeek TUI support multiple providers, reducing vendor dependency.
- **Hybrid**: Gemini CLI (Google) and Copilot CLI (GitHub/Microsoft) support multiple models but favor their ecosystem.

**3. Safety/Guardrails Philosophy:**
- **Aggressive**: Claude Code and OpenAI Codex have proprietary safety classifiers that generate false positives.
- **Minimal**: OpenCode, Pi, Qwen Code, DeepSeek TUI have fewer safety-related reports, suggesting lighter guardrails.

**4. Windows Investment:**
- **Weakest**: OpenAI Codex (most Windows issues), Claude Code (multiple Windows-specific bugs).
- **Strongest**: Gemini CLI (fewest Windows reports), DeepSeek TUI (BSD support included).
- **Improving**: OpenCode v2, Qwen Code are actively fixing Windows gaps.

---

## 5. Community Momentum & Maturity

| Tool | Momentum Signal | Maturity Level | Risk Factors |
|------|----------------|----------------|-------------|
| **Qwen Code** | Highest PR throughput (12); daemon architecture RFC; active CI patrol | Growing rapidly | CI instability; still evolving architecture |
| **Pi (mono)** | Fastest issue-to-close cycle; TUI v2 features; 10 PRs | Mature TUI; growing API | Small community; extension API gaps |
| **OpenCode** | 10 PRs; GPT-5.6 model support; v2 branch active | Mature but unstable (v2) | SQLite bloat critical; v2 sharp edges |
| **Gemini CLI** | 10 PRs; critical CVE fixes; eval framework | Mature with recent investment | Subagent false-success systemic |
| **DeepSeek TUI** | 10 PRs; i18n; provider expansion | Growing; well-structured | Small community, low engagement |
| **Claude Code** | High 👍 counts; broad issue diversity | Most mature, largest user base | Safety classifier backlash; slow issue resolution |
| **OpenAI Codex** | Strong engagement on agent hierarchy | Mature but rigid architecture | Model lock-in backlash; Windows stability |
| **Copilot CLI** | Moderate activity; TUI wedge visible | Mature but stability issues | Low PR throughput; session corruption |
| **Kimi Code** | Lowest activity; 2 PRs | Nascent | Very small community; Windows gaps |

### Key Observations:

- **Claude Code** and **OpenAI Codex** have the largest, most vocal communities but are **slower to iterate** on community-reported bugs. Their proprietary model focus creates both loyalty and frustration.

- **Qwen Code** has the **highest development velocity** (12 PRs) and is making bold architectural bets (multi-workspace daemon, background agents). The active CI patrol and rapid issue closure suggest strong project governance.

- **Pi** and **DeepSeek TUI** are **overperforming for their community size**—Pi's fast issue-to-close cycle and DeepSeek's i18n work indicate disciplined, responsive maintainership.

- **OpenCode v2** has the **most ambitious architecture** but is clearly unstable. The SQLite bloat issue (13GB+) is a production blocker that must be resolved for enterprise adoption.

- **Kimi Code CLI** is **lowest in all metrics**—few issues, few PRs, no releases, minimal community engagement. It may be a side project rather than a priority for MoonshotAI.

---

## 6. Trend Signals

### Signal 1: The "Vibe Coding" User Needs Guardrails
The emergence of "Teach Mode" requests (OpenCode #12675/#36521) and structured onboarding features reflects a growing segment of users who want guided AI coding experiences, not blank-slate tools. **Implication**: Tools that invest in onboarding, default safety profiles, and actionable feedback will capture casual and beginner users. Claude Code's safety over-alerting backlash shows the risk of getting guardrails wrong.

### Signal 2: Multi-Agent Economics Are Poorly Understood
OpenAI Codex's GPT-5.6 Sol forcing MultiAgent V2 (#31814, 121 👍) exposes a critical gap: **users cannot control the cost-latency-quality tradeoffs of multi-agent systems**. The `wait` tool burning tokens exponentially (#32640) and subagent false-success signals (Gemini #22323) show that the industry lacks good abstractions for agent orchestration economics. **Implication**: Tools that provide transparent agent cost dashboards and model selection controls will differentiate.

### Signal 3: Structured Output Is the New Battlefront
Headless JSON Schema failures (Claude Code #77026), MCP malformed JSON-RPC (OpenAI Codex #64654), and tool schema normalization (DeepSeek TUI #4346) indicate that **reliable structured data extraction is not solved**. As AI CLI tools move into CI/CD pipelines and automated workflows, broken structured output is a showstopper. **Implication**: Expect investment in formal tool-call validators, schema normalization layers, and retry-with-correction logic.

### Signal 4: Windows Is the Achilles' Heel of AI CLI Tools
Every tool has Windows-specific issues—file locking, terminal corruption, encoding failures, antivirus false positives. This isn't just a QA gap; it reflects a **fundamental architectural tension between Unix-native CLI tools and Windows process/UI models**. **Implication**: Tools written in Rust or Go (Pi, DeepSeek TUI) seem to have fewer Windows issues than Python or Node.js based tools (Kimi Code, Claude Code extension). Cross-platform testing infra investment will pay dividends.

### Signal 5: Persistent "AI Coworkers" Replace Stateless Chats
The convergence across Qwen Code (background agents), Pi (session lifecycle), OpenCode (daemon architecture), and Gemini CLI (auto-memory) toward **cross-session persistent context** signals a market shift. Users want AI that "remembers" project history, codebase state, and user preferences across sessions. **Implication**: The tools that deliver reliable, secure cross-session memory without data bloat (OpenCode's 13GB SQLite is the anti-pattern) will win long-term loyalty.

### Signal 6: Provider Agnosticism Wins—If Done Well
OpenCode and Pi—the most provider-agnostic tools—have among the highest community engagement and feature velocity. Meanwhile, Claude Code and OpenAI Codex face backlash from model lock-in (forced upgrades, safety classifiers, agent versioning). **Implication**: Users want the freedom to choose their model and switch providers. Tools that make multi-provider management simple (consistent tool schemas, unified pricing, transparent credential handling) will grow faster than single-provider tools, even if those providers have superior models.

### Signal 7: The MCP Plugin Gold Rush Is Here—But Buggy
MCP tool bridging, OAuth token forwarding, plugin lifecycle management—every tool is investing in plugin ecosystems, and every tool has integration bugs. The **lack of standardized credential bridging, tool discovery, and lifecycle management** across tools suggests the MCP specification itself may need refinement. **Implication**: The first tool to nail plugin reliability (consistent authentication, no schema conflicts, proper error propagation) will capture the plugin developer ecosystem.

---

## Summary for Decision-Makers

| If you prioritize... | Consider... | Because... |
|---------------------|-------------|------------|
| **Largest community, most resources** | Claude Code or OpenAI Codex | Largest user bases, best model access—but accept safety classifier risks and Windows gaps |
| **Fastest iteration, cutting-edge features** | Qwen Code or Pi | Highest PR velocity; Pi has fastest bug fixes, Qwen has boldest architecture |
| **Provider flexibility, no vendor lock-in** | OpenCode or DeepSeek TUI | True multi-provider support; OpenCode has larger community, DeepSeek has cleaner codebase |
| **Windows compatibility** | Gemini CLI or DeepSeek TUI | Fewer Windows-specific issues; Rust/TUI-native architectures |
| **Production CI/CD reliability** | Pi or DeepSeek TUI (with caution) | Best structured output handling; Pi's fast fix cycle reduces blast radius |
| **Enterprise/collaborative features** | Qwen Code (daemon) or Copilot CLI (GitHub integration) | Qwen's multi-workspace daemon; Copilot's GitHub ecosystem |
| **Cost-conscious/small team** | DeepSeek TUI or Kimi Code CLI | Lower overhead; DeepSeek has broader provider support |

The AI CLI tools landscape is **still pre-paradigmatic**—no single tool has converged on the "right" architecture, model strategy, or plugin model. The next 6–12 months will likely see consolidation around daemon architectures, structured output reliability, and cross-session persistence. Windows pain will drive Rust/Go adoption. Safety over-alerting will drive demand for transparent, user-controllable guardrails.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-13 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following pull requests represent the most-discussed Skill submissions by comment volume and community engagement:

### #1298 — fix(skill-creator): run_eval.py always reports 0% recall
- **Functionality**: Fixes the core evaluation script used by the skill-creator optimization loop. Patches artifact installation, Windows stream handling, trigger detection, and parallel worker behavior. Without this fix, the entire description-optimization pipeline optimizes against noise (always reporting 0% recall).
- **Discussion highlights**: Addresses issue #556 (10+ independent reproductions). The community has extensively debated root cause — the evaluation pipeline creates synthetic command files in `.claude/commands/` but Claude Code's `-p` mode never triggers those commands during eval.
- **Status**: Open | [PR #1298](https://github.com/anthropics/skills/pull/1298)

### #514 — Add document-typography skill
- **Functionality**: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses the gap where LLMs produce correct content but poor typographic layout.
- **Discussion highlights**: Strong consensus that these issues affect every Claude-generated document. Community members contributed additional typographic edge cases (hyphenation rules, justified text spacing).
- **Status**: Open | [PR #514](https://github.com/anthropics/skills/pull/514)

### #723 — feat: add testing-patterns skill
- **Functionality**: Comprehensive testing skill covering the Testing Trophy model, AAA pattern, React Testing Library, end-to-end testing with Playwright, and property-based testing. Defines what to test vs. what NOT to test.
- **Discussion highlights**: Debates over framework-specific vs. framework-agnostic testing guidance. Community requested additional sections for mocking strategies and snapshot testing best practices.
- **Status**: Open | [PR #723](https://github.com/anthropics/skills/pull/723)

### #1367 — feat(skills): add self-audit skill (v1.3.0)
- **Functionality**: A universal output auditing skill performing mechanical file verification followed by a four-dimension reasoning quality audit in damage-severity priority order. Works with any project, tech stack, or model.
- **Discussion highlights**: Community feedback focused on the audit dimensions taxonomy (factual accuracy, logical coherence, completeness, safety). Requests for configurable severity thresholds.
- **Status**: Open | [PR #1367](https://github.com/anthropics/skills/pull/1367)

### #486 — Add ODT skill (OpenDocument text creation)
- **Functionality**: Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Includes template filling and ODT-to-HTML conversion. Triggers on mentions of ODT/ODS/ODF/LibreOffice.
- **Discussion highlights**: Discussion around template variable syntax and LibreOffice compatibility. Community requested OpenFormula spreadsheet support as a follow-up.
- **Status**: Open | [PR #486](https://github.com/anthropics/skills/pull/486)

### #83 — Add skill-quality-analyzer and skill-security-analyzer
- **Functionality**: Meta-skills for evaluating other Skills across five quality dimensions (Structure & Documentation, Trigger Precision, etc.) and security analysis for trust boundary verification.
- **Discussion highlights**: Directly connected to Issue #492 (security/trust concerns). Community emphasized needing security scanning before the skills marketplace expands further.
- **Status**: Open | [PR #83](https://github.com/anthropics/skills/pull/83)

### #509 — docs: add CONTRIBUTING.md
- **Functionality**: Addresses the community health gap — the repo scored 25% on GitHub's community health metrics. Adds five sections including skill naming conventions, review process, and testing requirements.
- **Discussion highlights**: Closes Issue #452. Community contributors noted this is a prerequisite for scaling community submissions. Debates over required CI checks for new Skills.
- **Status**: Open | [PR #509](https://github.com/anthropics/skills/pull/509)

### #210 — Improve frontend-design skill clarity
- **Functionality**: Revises the frontend-design skill to ensure every instruction is actionable within a single conversation. Adds specificity for layout, color, typography, and responsive design decisions.
- **Discussion highlights**: Community feedback focused on making the skill less prescriptive — balancing "rules to follow" with "patterns to consider." Requests for accessibility-focused sub-sections.
- **Status**: Open | [PR #210](https://github.com/anthropics/skills/pull/210)

---

## 2. Community Demand Trends

The most-anticipated new Skill directions, distilled from Issues with the highest engagement:

| Demand Category | Key Issues | Community Sentiment |
|---|---|---|
| **Security & Trust Validation** | #492 (34 comments), #1175 | Highest urgency — the community is alarmed by trust boundary abuse under the `anthropic/` namespace. Demand for Skill signing, permission manifests, and security scanning before marketplace expansion. |
| **Skill-Creator Toolchain Stability** | #556 (12 comments), #1169, #1061 | Cross-cutting demand for fixing the evaluation pipeline. Multiple Windows compatibility issues and the 0% recall bug block all Skill optimization work. |
| **Enterprise & Org Sharing** | #228 (14 comments) | Demand for organizational skill libraries, sharing links, and group-managed skill repositories. |
| **Reasoning Quality & Governance** | #412, #1385, #1362 | Growing interest in AI output auditing — quality gates, adversarial review pipelines, and safety patterns for agent systems. |
| **Format Expansion** | #1329 (compact-memory), #189 (plugin dedup) | Niche but passionate demand for symbolic notation for agent state, and fixing duplicate skill installations. |

---

## 3. High-Potential Pending Skills

These PRs have active discussion threads and may land soon:

| PR | Skill | Why It Has Momentum |
|---|---|---|
| [#1367](https://github.com/anthropics/skills/pull/1367) | self-audit (reasoning quality gate) | Author has follow-up issue (#1385) proposing pipeline extension; active iteration within last 10 days |
| [#1302](https://github.com/anthropics/skills/pull/1302) | color-expert (color naming systems, spaces) | Self-contained, well-defined domain; author is established contributor (meodai) |
| [#1261](https://github.com/anthropics/skills/pull/1261) | fix(skill-creator): isolate eval files from live project | Directly unblocks the entire skill-creation pipeline; addresses #1260 |
| [#1099](https://github.com/anthropics/skills/pull/1099) | fix(skill-creator): Windows subprocess crash | Combined with #1050, this resolves Windows compatibility blockers |
| [#181](https://github.com/anthropics/skills/pull/181) | SAP-RPT-1-OSS predictor | Enterprise ML integration; well-defined use case with SAP ecosystem |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for toolchain reliability (fixing the skill-creator evaluation pipeline) and trust infrastructure (security auditing, quality gates, and org-level governance) — before expanding the Skill catalog further, contributors need confidence that Skills can be built, tested, and distributed safely.**

---

# Claude Code Community Digest — 2026-07-13

## Today's Highlights
No new releases were shipped in the last 24 hours, but the community remains highly engaged with several long-running bugs gaining significant traction. The top stories this week are a critical permissions bypass in the VS Code extension, a **claude-fable-5** advisor tool collapse at high token counts, and a surge of reports around **false-positive safety classifiers** interrupting legitimate development workflows across multiple domains.

---

## Releases
**None.** No new versions tagged in the last 24 hours.

---

## Hot Issues

### 1. VS Code Extension: Permissions Not Respected
**#15921** — `[BUG] VSCode Extension: .claude/settings.local.json permissions not respected for Bash/Write/Edit operations (even with bypassPermissions mode)`  
**Why it matters:** This is the single most-commented open issue (28 comments, 28 👍). The `bypassPermissions` mode was designed to suppress permission prompts for trusted workflows; if even that flag is ignored, users on Windows have no reliable way to automate file writes from the extension.  
**Community reaction:** High frustration — several workarounds posted but no official fix acknowledged.  
🔗 [Issue #15921](https://github.com/anthropics/claude-code/issues/15921)

### 2. Advisor Tool "unavailable" at 100K Tokens on claude-fable-5
**#67609** — `Advisor tool returns "unavailable" on claude-fable-5 whenever transcript exceeds ~100K tokens`  
**Why it matters:** The advisor tool is a core UX differentiator — it provides inline suggestions as you code. When it silently stops working beyond 100K tokens, users lose a key productivity feature mid-session. 20 comments, 38 👍 indicate this is a widely encountered regression.  
**Community reaction:** Users confirm the issue is reproducible across macOS and that the same config works fine below the threshold.  
🔗 [Issue #67609](https://github.com/anthropics/claude-code/issues/67609)

### 3. GitHub MCP Plugin: Malformed JSON-RPC Payload
**#64654** — `plugin:github:github MCP fails with HTTP 400 — malformed JSON-RPC payload missing version tag`  
**Why it matters:** The official GitHub MCP plugin is breaking for many users on macOS. 16 comments, 41 👍. A missing `jsonrpc` version field in the payload suggests a serialization bug in the plugin layer, not user error.  
**Community reaction:** Several users report the same failure with different GitHub operations; root cause is still under investigation.  
🔗 [Issue #64654](https://github.com/anthropics/claude-code/issues/64654)

### 4. Ctrl+C Copy Fails in VS Code Extension Chat
**#43477** — `Copying text (Ctrl+C) from Claude Code window in VS Code fails`  
**Why it matters:** A fundamental UX bug — cannot copy code or responses out of the chat panel. 14 comments, 2 👍. Windows-only, still open after 3 months.  
**Community reaction:** Quiet but persistent; users describe the workaround of right-click → copy as "annoying."  
🔗 [Issue #43477](https://github.com/anthropics/claude-code/issues/43477)

### 5. Model Downgraded to Opus 4.8 Due to Pet Food Content
**#77006** — `Model automatically downgraded from Claude Fable 5 to Claude 3 Opus 4.8 due to pet food content analysis`  
**Why it matters:** This is a striking example of an overly aggressive safety classifier. A user analyzing pet food labels was silently downgraded from the latest premium model to an older, weaker one.  
**Community reaction:** High-vote mockery in comments — "totally stupid," "biology hazard" false positive.  
🔗 [Issue #77006](https://github.com/anthropics/claude-code/issues/77006)

### 6. Cowork Sandbox Fails on Windows After SDK Update
**#76094** — `Cowork sandbox fails at sdk_install on Windows — VM guest crashes with "connection forcibly closed" (regression SDK 2.1.181 → 2.1.202)`  
**Why it matters:** A confirmed regression in the cowork/sandbox feature for Windows. 5 comments, 0 👍 (low visibility but high impact for affected users).  
**Community reaction:** Bisected to a specific SDK range; no hotfix yet.  
🔗 [Issue #76094](https://github.com/anthropics/claude-code/issues/76094)

### 7. Click-Through Submits Unintended Permission Answers
**#76743** — `Windows: click-to-focus activates pending permission dialog option (click-through), submitting an unintended answer`  
**Why it matters:** A dangerous UX flaw — if a permission dialog is pending and the window is not focused, clicking the window to focus it also submits the dialog's default action (e.g., "Deny"). 4 comments.  
**Community reaction:** Users call it "a security risk in itself" because it can silently deny legitimate operations.  
🔗 [Issue #76743](https://github.com/anthropics/claude-code/issues/76743)

### 8. Cybersecurity False Positives Blocking Minecraft Modding
**#65891** — `Cybersecurity protection blocks Claude model execution during code writing`  
**Why it matters:** Multiple reports (see also #65890, #65892, #77002) show that legitimate development — Minecraft modding, git push, arithmetic — triggers "cyber-related safeguards." These are closed as stale but the pattern is alarming for any developer working in game dev, security-adjacent, or checkpointing tools.  
**Community reaction:** Users are frustrated that they cannot even read source files from open-source projects (DMTCP, Minecraft).  
🔗 [Issue #65891](https://github.com/anthropics/claude-code/issues/65891)

### 9. RTL Text Rendering Broken in VS Code Chat
**#75196** — `Chat panel doesn't render RTL text (Persian/Arabic/Hebrew) correctly`  
**Why it matters:** A11y and localization issue. The chat webview doesn't detect text direction, making conversations in RTL languages unreadable. 1 comment, 1 👍 — but represents a significant gap for non-English developers.  
**Community reaction:** Reported as a "missing direction detection" — the fix is likely a CSS `dir="auto"` attribute.  
🔗 [Issue #75196](https://github.com/anthropics/claude-code/issues/75196)

### 10. Headless JSON Schema: Array Property Serialized as XML
**#77026** — `[BUG] Headless --json-schema: model serializes an array property as XML text inside a string property, then either retry-exhausts or silently accepts a placeholder`  
**Why it matters:** Freshly filed (0 comments) but critical for anyone using `--json-schema` in headless/CI pipelines. The model is serializing structured output in the wrong format, then either exhausting retries or producing silent incorrect output.  
**Community reaction:** Too new for discussion, but the implications for reliable structured data extraction are serious.  
🔗 [Issue #77026](https://github.com/anthropics/claude-code/issues/77026)

---

## Key PR Progress

### 1. #76986 — Fix: Preserve Existing Labels When Auto-Closing Duplicates
**What it does:** The auto-close script was replacing all labels with just `["duplicate"]`. This fix preserves original labels to maintain issue categorization.  
🔗 [PR #76986](https://github.com/anthropics/claude-code/pull/76986)

### 2. #76985 — Fix: Read Full Multi-Line Description in Plugin Validator
**What it does:** The `validate-agent.sh` script now reads the full multi-line description from frontmatter (used to truncate at the first newline).  
🔗 [PR #76985](https://github.com/anthropics/claude-code/pull/76985)

### 3. #15165 — Update README.md (docs link fix)
**What it does:** Fixes a broken documentation URL in the project README. Closed, merged.  
🔗 [PR #15165](https://github.com/anthropics/claude-code/pull/15165)

*Note: Only 3 PRs were active in the last 24h — two open fixes and one historical doc fix.*

---

## Feature Request Trends

### 1. Terminal Word-Wrapping Control (TUI)
**#43113** — Users want a flag to **disable hard newline insertion** and let the terminal handle word-wrapping for markdown/prose output. 51 👍 — the most upvoted open feature request.  
🔗 [Issue #43113](https://github.com/anthropics/claude-code/issues/43113)

### 2. Agent View: Show Project/Repo Per Session
**#69449** — FleetView (`claude agents`) should display the **cwd** per session row, not just one global header. Essential for managing sessions across multiple projects. 3 👍.  
🔗 [Issue #69449](https://github.com/anthropics/claude-code/issues/69449)

### 3. Agent View: Require Manual Completion (No Auto-Archive)
**#58215** — Users want to **prevent agent sessions from auto-completing**. Closed as stale but the idea persists: keep sessions open until explicitly archived.  
🔗 [Issue #58215](https://github.com/anthropics/claude-code/issues/58215)

### 4. VS Code Extension: Desktop-App-Level Status Indicators
**#77003** — Show **model name, Ultracode/mode, effort, and usage tokens** next to the chat input in the VS Code extension, matching the desktop app.  
🔗 [Issue #77003](https://github.com/anthropics/claude-code/issues/77003)

### 5. Model Version Pinning
**#65888** — Request to **pin a specific model snapshot** (e.g., `opus-4-7` as of May 15) to guarantee reproducible behavior across silent Anthropic API updates. Closed as stale, but the need is clear from user reports of behavioral drift.  
🔗 [Issue #65888](https://github.com/anthropics/claude-code/issues/65888)

---

## Developer Pain Points

### 1. False-Positive Safety/AUP Classifiers
The #1 pain point by frequency. Multiple issues (#65873, #65891, #65890, #77002, #77006) describe **legitimate development workflows interrupted** by safety classifiers — trading app development on testnet, Minecraft modding, pet food analysis, git push, and even simple arithmetic. Users report **model downgrades** (Fable 5 → Opus 4.8) and **complete session termination** without recourse.

### 2. Cowork + Sandbox Regressions on Windows
Windows users are hit hardest this week: the **cowork sandbox** crashes after an SDK update (#76094), **trusted-folder validation** rejects shared drive roots (#76254), and the **new project folder picker** is replaced with an upload-only chat menu after a Chat/Cowork merge (#76694). The Windows TUI also has a **click-through vulnerability** in permission dialogs (#76743).

### 3. Permissions System Inconsistencies
The permissions system has multiple bugs: rules under `~/.claude/` show as loaded but never match at runtime (#57132), and the VS Code extension ignores `settings.local.json` permissions entirely (#15921). This undermines trust in the permission model as a whole.

### 4. Model Output Reliability in Structured Formats
The **Headless JSON Schema** bug (#77026) and the **GitHub MCP plugin** malformed JSON-RPC (#64654) both indicate that structured output serialization is fragile — the model sometimes emits XML instead of JSON, or omits required fields. For CI/CD and headless use cases, this is a showstopper.

### 5. VS Code Extension UX Gaps
The VS Code extension lags behind the desktop app in several areas: **no copy** (Ctrl+C fails, #43477), **no RTL text support** (#75196), **no status indicators** (#77003), and **permissions not respected** (#15921). For many developers, the VS Code extension is their primary interface; these gaps are a significant source of friction.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-13

## Today's Highlights

The community continues to experience significant friction with GPT-5.6 Sol's aggressive agent hierarchy, where model metadata overrides user configuration to force MultiAgent V2 and hide subagent controls. Windows stability remains a major concern, with several crashes, freezing, and sandbox setup failures reported. A security-oriented PR closing PAT token injection paths stands out as a critical infrastructure improvement.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#31814 — GPT-5.6 Sol forces all subagents to Sol instances](https://github.com/openai/codex/issues/31814)**  
   *56 comments, 121 👍*  
   The most upvoted open issue. GPT-5.6 Sol's model metadata overrides the `multi_agent_version` feature toggle, forcing MultiAgent V2 which hides subagent model configuration. Users cannot specify non-Sol models for subagents, creating an expensive lock-in. Community reaction is strongly negative.

2. **[#18960 — Frequent websocket reconnect loop in Codex App](https://github.com/openai/codex/issues/18960)**  
   *51 comments, 39 👍*  
   Persistent streaming failure on macOS Pro. The server closes websockets before responses complete, causing infinite reconnection loops. Long-running (3+ months) with no fix yet.

3. **[#20214 — Codex App freezes on Windows 11 despite sufficient resources](https://github.com/openai/codex/issues/20214)**  
   *34 comments, 48 👍*  
   AMD Ryzen 5 with 32GB RAM still experiences stuttering and freezes. High priority due to broad Windows impact.

4. **[#25271 — Computer Use cannot determine Chrome URL on Windows](https://github.com/openai/codex/issues/25271)**  
   *17 comments, 8 👍*  
   Chrome tab detection broken on Windows, even on `chrome://newtab/`. Breaks browser automation workflows.

5. **[#31097 — GPT-5.5 forces MultiAgentV2 despite disable flag](https://github.com/openai/codex/issues/31097)**  
   *6 comments, 6 👍*  
   Older model also exhibits the same agent override behavior as #31814. Suggests a systemic architecture issue, not just Sol-specific.

6. **[#32095 — GPT-5.6 Sol false-positive safety flag on normal request](https://github.com/openai/codex/issues/32095)**  
   *5 comments, 3 👍*  
   Pro 20x user reports a false "cybersecurity activity" alert on a routine code request. Safety checks are over-aggressive with Sol.

7. **[#32640 — Built-in `wait` tool capped at ~50s causes massive token burn](https://github.com/openai/codex/issues/32640)**  
   *4 comments*  
   MultiAgent V2 re-samples every 50 seconds when using `wait`, burning tokens exponentially on long waits. Critical for agent workflows.

8. **[#31944 — `codex app` ignores unified ChatGPT.app on macOS, creates duplicate](https://github.com/openai/codex/issues/31944)**  
   *4 comments, 7 👍*  
   After the July 9 merge of Codex into ChatGPT.app, the CLI still looks for `Codex.app` and downloads a separate installer. Confusing for users.

9. **[#32653 — Codex Desktop crashes entirely on missing MCP tool call result](https://github.com/openai/codex/issues/32653)**  
   *3 comments*  
   Post-update crash when tool call result is missing. Unhandled exception takes down the entire app.

10. **[#32331 — Norton 360 flags Codex as malware on Windows](https://github.com/openai/codex/issues/32331)**  
    *2 comments, 2 👍*  
    Simply opening an existing thread triggers Norton Behavioral Protection (IDP.HELU.PSE80%s_cmd). Undermines user trust in the application.

## Key PR Progress

1. **[#29898 — Preserve PAT auth against host token injection](https://github.com/openai/codex/pull/29898)**  
   *CLOSED* — Rejects `chatgptAuthTokens` when PAT auth is active. Includes regression tests and 401 recovery coverage. Security-critical infrastructure fix.

2. **[#30504 — Edit previous prompts using session forks](https://github.com/openai/codex/pull/30504)**  
   *OPEN* — Replaces destructive `thread/rollback` with branching via session forks. Enables non-destructive prompt editing in TUI. Addresses a long-standing UX complaint.

3. **[#32628 — Improve composer completion target resolution](https://github.com/openai/codex/pull/32628)**  
   *CLOSED* — Bot-authored fix for `@` and `$` completion targets. Handles atomic text boundaries and conflict resolution between file/skill/plugin candidates. Improves IDE-like editing.

## Feature Request Trends

- **AGENTS.local overlays with @-reference expansion** (#28739) — Users want additive (not replacement) instruction files and cross-file reference resolution similar to Claude Code. 4 comments, moderate interest.
- **On-demand automation triggers** (#28064) — Request for "run now" buttons on scheduled automations. Low activity but represents a clear usability gap.
- **Source file attribution/provenance** (#28739, same issue) — Being able to trace which AGENTS file contributed which instruction, akin to Claude's provenance features.

## Developer Pain Points

- **Agent model hierarchy overrides** dominate discussion. Both GPT-5.5 and GPT-5.6 Sol ignore explicit user configuration for subagent models. Workarounds are non-existent.
- **Windows platform instability** is a recurring theme: sandbox setup stuck (#32492), Remote Control enrollment failure (#31387, #32164), app crashes on MCP errors (#32653), browser/webview crashes (#30178), and Chrome URL detection broken (#25271).
- **Remote pairing/SSH issues** persist across platforms: "No chats" on SSH remotes (#27284), Windows Remote Control stuck in "Reconnecting..." (#31973), and worktree threads not grouped (#32082).
- **Safety over-alerting** (#32095, #32331) — False positives from Sol's safety checks and third-party antivirus flagging suggest the app's execution patterns look suspicious to external security tools.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — July 13, 2026

## Today's Highlights
No new releases landed today, but the repository saw heavy activity around dependency upgrades and critical security patches. Two open PRs address **CVE-2026-47429** (Vitest) and **CVE-2026-9277** (shell-quote), both rated CRITICAL. On the bug front, a long-standing subagent false-success issue (#22323) continues to gather comments, and a new Windows-specific terminal corruption bug (#28370) was filed just yesterday.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10 by Comment Activity)

1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` despite hitting the maximum turn limit before performing any analysis. This is a **critical reliability bug** — users cannot trust subagent completion signals. 10 comments, 2 👍.

2. **[#24353 — Robust component level evaluations (EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   An EPIC tracking 76 behavioral eval tests across 6 supported Gemini models. Aims to mature the evaluation harness introduced in #15300. 7 comments.

3. **[#22745 — AST-aware file reads, search, and mapping (EPIC)](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   Investigates whether AST-aware tools can reduce token waste, misaligned reads, and improve codebase navigation. Potential to **reduce turn count** and improve accuracy. 7 comments.

4. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   A high-severity P1 bug: the generalist agent hangs indefinitely on simple tasks (e.g., folder creation). Workaround exists (disable subagent delegation). 7 comments, 8 👍 — highest community engagement today.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   Anecdotal but corroborated: custom skills and sub-agents are rarely invoked autonomously. Users must explicitly instruct the model. 6 comments.

6. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   A memory system design flaw: sessions the extractor agent chooses to skip are never marked as processed, causing infinite re-examination. 5 comments.

7. **[#25166 — Shell command hangs with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   P1 bug: simple shell commands (that don't prompt for input) leave the CLI stuck in a "Waiting input" state. 4 comments.

8. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   Termination reason "GOAL" but no useful work done — possible Wayland-specific rendering issue. 4 comments.

9. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   Security concern: secrets are sent to the model before the extraction prompt attempts redaction. Also, logging leaks skill configurations. 3 comments.

10. **[#28370 — Windows full-history replay (C-Dump) on resize/hot-reload](https://github.com/google-gemini/gemini-cli/issues/28370)**  
    Newly filed: terminal resizes cause the entire chat history to be dumped to stdout on Windows. High annoyance for Windows users. 1 comment.

## Key PR Progress (Top 10)

1. **[#28369 — Local eval report command + developer docs](https://github.com/google-gemini/gemini-cli/pull/28369)**  
   Adds `npm run eval:report` to aggregate pass rates from Vitest `report.json` across models. Improves developer workflow for behavioral evals.

2. **[#28368 — Upgrade vitest to 4.1.0 (CVE-2026-47429)](https://github.com/google-gemini/gemini-cli/pull/28368)**  
   **CRITICAL** CVE fix. Upgrades from 3.2.4 → 4.1.0. Need-issue label suggests missing tracking link.

3. **[#28367 — Upgrade shell-quote to 1.8.4 (CVE-2026-9277)](https://github.com/google-gemini/gemini-cli/pull/28367)**  
   **CRITICAL** CVE fix. Targets command-injection vulnerability in shell argument parsing.

4. **[#28366 — Tidy implementation detail (#28340)](https://github.com/google-gemini/gemini-cli/pull/28366)**  
   Small scoped P1 patch for an undefined behavior fix.

5. **[#28365 — Fix tools.core wildcard deny blocking MCP tools](https://github.com/google-gemini/gemini-cli/pull/28365)**  
   **Important bug fix:** Setting `tools.core: []` silently disabled all MCP tools regardless of trust settings. Adds `builtinOnly` flag to policy rules.

6. **[#28364 — Deep-merge user model config over defaults](https://github.com/google-gemini/gemini-cli/pull/28364)**  
   Fixes shallow-spread merge that broke nested `modelConfigServiceConfig` overrides.

7. **[#28363 — Prevent AbortSignal listener leak in ShellExecutionService](https://github.com/google-gemini/gemini-cli/pull/28363)**  
   Memory leak fix: removes `AbortSignal` listeners when a process finishes naturally. Fixes #28280.

8. **[#28383 — Bump @types/node 20.11.24 → 26.1.0](https://github.com/google-gemini/gemini-cli/pull/28383)**  
   Major version bump for Node.js type definitions — aligns with modern Node APIs.

9. **[#28382 — Bump puppeteer-core 24.0.0 → 25.3.0](https://github.com/google-gemini/gemini-cli/pull/28382)**  
   Major browser automation upgrade. Likely impacts browser subagent stability.

10. **[#28381 — Bump js-yaml 4.1.1 → 5.2.1](https://github.com/google-gemini/gemini-cli/pull/28381)**  
    Major YAML parser upgrade — breaking changes possible (new `safeLoad`/`load` semantics).

## Feature Request Trends
- **AST-aware tooling** (#22745, #22746): Multiple EPICs explore replacing naive file reads with AST-aware tools to reduce token waste and improve codebase mapping precision.
- **Subagent trajectory sharing** (#22598): Users want agent internals visible via `/chat share` for debugging and eval scenarios.
- **Agent self-awareness** (#21432): Community wants agents to know their own CLI flags, hotkeys, and execution mechanics to act as self-documenting tools.
- **Destructive operation prevention** (#22672): Demand for guardrails against `git reset --force`, dangerous DB operations, and other destructive commands.
- **Browser agent resilience** (#22232): Auto-session takeover and lock recovery for persistent browser profiles — currently fail-fast only.

## Developer Pain Points
1. **Subagent false success signals** (#22323, #21983): Subagents report `GOAL` success after hitting turn limits or failing silently — eroding trust in autonomous mode.
2. **Hangs and stuck states** (#21409, #25166, #22465): CLI hangs on simple shell commands, Vite scaffolding, and generalist delegation. Chronic frustration.
3. **Windows terminal corruption** (#28370): Full-history replay (C-Dump) on resize/hot-reload — Windows users face degraded UX.
4. **Memory system over-processing** (#26522, #26525): Auto Memory retries low-signal sessions forever and sends secrets to model context before redaction.
5. **Tool/agent configuration fragility** (#24246, #20079, #22093): Symlinks not recognized as agents, 400 errors with >128 tools, subagents running despite being disabled.
6. **MCP tool trust model broken** (#28365 fix): Wildcard deny rules unintentionally disabled all MCP tools — fundamental authorization flaw.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-13

## Today's Highlights
A surge of critical stability issues hit the repository over the past 24 hours, with a V8 native crash during tool-heavy sessions (#4102) and a TUI wedge bug in WSL2 (#4069) drawing the most community attention. Seven new triage issues were filed, revealing regressions in plugin authentication, session persistence, and MCP tool bridging. No new releases were published.

## Releases
No new releases in the last 24 hours. Latest available version remains `1.0.70-0`.

## Hot Issues

1. **#4102 — Native V8 array-length crash during active tool-heavy turns and session resume**  
   *Author: RollsChris | Updated: 2026-07-12 | 👍: 0*  
   The packaged Linux x64 binary aborts inside V8 during heavy tool use and session resume. Originally blamed on concurrent resumes, further testing disproved that theory. Critical because it corrupts the process irrecoverably.  
   [View Issue](https://github.com/github/copilot-cli/issues/4102)

2. **#4069 — TUI wedges mid-turn (screen clears, input dead, Ctrl+C ignored) — WSL2 + Windows Terminal**  
   *Author: msmbaldwin | Updated: 2026-07-12 | 👍: 8*  
   The terminal becomes completely unresponsive during active streaming with `claude-opus-4.7`. EIO on stdout followed by EPIPE on the JSON-RPC transport. Highest community reaction score in this batch.  
   [View Issue](https://github.com/github/copilot-cli/issues/4069)

3. **#4024 — Voice mode: all bundled ASR models fail silently**  
   *Author: sylvanc | Updated: 2026-07-12 | 👍: 0*  
   Recording works (confirmed via PulseAudio capture) but every transcription returns empty for all three Nemotron models. Root cause suspected in `MultiModalProcessor` routing for RNNT in Foundry Local Core.  
   [View Issue](https://github.com/github/copilot-cli/issues/4024)

4. **#4098 — Resuming a session can leave truncated and concatenated events in events.jsonl**  
   *Author: Adamkadaban | Updated: 2026-07-12 | 👍: 0*  
   Malformed JSONL records prevent resumed sessions from being resumed again. Three physical lines contained incomplete event prefixes concatenated without separators.  
   [View Issue](https://github.com/github/copilot-cli/issues/4098)

5. **#4097 — apply_patch stores deleted binary in session history, permanently exceeding 5 MB limit**  
   *Author: Adamkadaban | Updated: 2026-07-12 | 👍: 0*  
   Deleting a large binary file via `apply_patch` stores the full binary as a text diff in `result.detailedContent`. Breaks `/compact` and causes subsequent requests to fail against CAPI Responses' 5 MB limit.  
   [View Issue](https://github.com/github/copilot-cli/issues/4097)

6. **#4103 — Plugin marketplace clone disables Git credential helpers, breaking private HTTPS repos**  
   *Author: arnab9211 | Updated: 2026-07-12 | 👍: 0*  
   Adding a plugin marketplace from private Azure DevOps HTTPS repos fails. Likely regression from v1.0.70's "fail fast when marketplace plugin git auth needed" change.  
   [View Issue](https://github.com/github/copilot-cli/issues/4103)

7. **#4101 — write_agent may block until background agent starts processing, queuing new user input**  
   *Author: xieyubo | Updated: 2026-07-12 | 👍: 0*  
   Calling `write_agent` on an idle background agent does not return control until the target agent wakes up. User input during this wait is silently queued.  
   [View Issue](https://github.com/github/copilot-cli/issues/4101)

8. **#4094 — Deleting a session in the app doesn't remove it from session-store.db (orphaned session)**  
   *Author: evdbogaard | Updated: 2026-07-12 | 👍: 0*  
   UI deletion does not propagate to shared `~/.copilot` store. Leaves orphaned records in `data.db`, `session-store.db`, and VS Code metadata cache.  
   [View Issue](https://github.com/github/copilot-cli/issues/4094)

9. **#4095 — Windows: plugin update fails with "Access is denied (os error 5)" while VS Code is running**  
   *Author: FBakkensen | Updated: 2026-07-12 | 👍: 0*  
   Copilot extension's watcher handles on `installed-plugins` directory block updates. Git fetch succeeds, but file operations fail on Windows file locking.  
   [View Issue](https://github.com/github/copilot-cli/issues/4095)

10. **#4096 — Third-party MCP server shows "Connected" but tools missing from CLI sessions (OAuth token never bridged)**  
    *Author: bugale | Updated: 2026-07-12 | 👍: 0*  
    Atlassian Remote MCP shows green "Connected" badge in app UI, but tools never appear in CLI sessions. OAuth token acquired by the app is not forwarded to the spawned CLI agent.  
    [View Issue](https://github.com/github/copilot-cli/issues/4096)

## Key PR Progress

1. **#4100 — shangti0168 (by huangyoufeng76-debug)**  
   Security-related PR. No detailed description provided. Minimal community engagement.  
   [View PR](https://github.com/github/copilot-cli/pull/4100)

Note: Only one PR was updated in the last 24 hours.

## Feature Request Trends

- **Plugin ecosystem improvements**: Multiple issues request better Git credential handling for private HTTPS repos (#4103) and Windows file-locking compatibility for plugin updates (#4095).
- **Session management**: Persistent requests for proper session deletion propagation (#4094) and session resume reliability (#4098, #4097).
- **MCP tool interop**: Demand for proper OAuth token bridging from the app UI to CLI sessions (#4096).
- **Multi-agent coordination**: Interest in non-blocking `write_agent` behavior to avoid user input queuing (#4101).

## Developer Pain Points

1. **Terminal stability on WSL2** — The TUI wedge issue (#4069) with 8 upvotes reflects a recurring pain point for Windows developers running Copilot CLI under WSL2 with Windows Terminal.
2. **Session corruption on resume** — Two distinct issues (#4098, #4097) show that session persistence is fragile, especially with large binary files or interrupted writes.
3. **Plugin update friction** — Windows file locking (#4095) and Git credential helper disabling (#4103) create barriers for plugin users.
4. **Voice mode non-functionality** — ASR models failing silently (#4024) with no user feedback is frustrating for voice-first workflows.
5. **Memory limits from tool output** — Binary content stored in session history (#4097) is a systemic design problem that can make long sessions unusable.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date:** 2026-07-13

## 1. Today's Highlights
The Kimi Code CLI community had a quiet day with no new releases or intense activity, but two long-standing pull requests saw updates, signaling ongoing refinement. A critical bug regarding TPD rate limit calculations remains open and unresolved, causing concern among heavy users. The main development focus is on improving Windows compatibility and handling non-UTF-8 output from child processes.

## 2. Releases
None. No new versions were published in the last 24 hours.

## 3. Hot Issues

1. **#2318 [OPEN] [bug] request reached organization TPD rate limit, current: 1505241**  
   *Author: globalvideos272-lab | 👍: 1*  
   A critical bug report concerning incorrect TPD (Tiered Performance Degradation) rate limit calculations when using kimi 2.6 on Windows 10 with the moonshot.ai platform. The user reports hitting a limit of 1.5M, which appears to be a miscalculation rather than an actual cap. This is a high-priority issue as it directly blocks users from accessing the service.  
   **Link:** [Issue #2318](https://github.com/MoonshotAI/kimi-cli/issues/2318)

4. **#2178 [OPEN] [bug] Windows binary missing version info**  
   *Author: he-yufeng*  
   Reported that Windows executable artifacts lack proper FileVersionInfo metadata, causing compatibility issues with enterprise deployment tools and antivirus software. This issue has already been addressed by PR #2181.  
   **Link:** [Issue #2178](https://github.com/MoonshotAI/kimi-cli/issues/2178)

5. **#2313 [OPEN] [bug] UnicodeDecodeError on Windows with locale-encoded output**  
   *Author: he-yufeng*  
   Worker processes on Windows emitting cp1252 or other locale-encoded bytes cause a strict UTF-8 decoder to fail, masking real worker failures. The fix is under review in PR #2350.  
   **Link:** [Issue #2313](https://github.com/MoonshotAI/kimi-cli/issues/2313)

## 4. Key PR Progress

1. **#2181 [OPEN] fix: add Windows binary version info**  
   *Author: he-yufeng | Updated: 2026-07-12*  
   Adds a PyInstaller Windows version-info file generated from `pyproject.toml`, ensuring both one-file and one-dir builds include proper FileVersionInfo. The PR also adds a CI assertion to prevent future regressions. This is a critical quality-of-life fix for Windows users.  
   **Link:** [PR #2181](https://github.com/MoonshotAI/kimi-cli/pull/2181)

2. **#2350 [OPEN] fix: tolerate non-utf8 worker output**  
   *Author: he-yufeng | Updated: 2026-07-12*  
   Addresses the UnicodeDecodeError on Windows by decoding worker stdout and crash stderr more gracefully. Instead of strict UTF-8, it will now handle locale-encoded bytes (e.g., cp1252) and report errors without hiding the underlying worker failure.  
   **Link:** [PR #2350](https://github.com/MoonshotAI/kimi-cli/pull/2350)

## 5. Feature Request Trends
No significant new feature requests were surfaced in the last 24 hours. The community's focus remains on reliability and platform compatibility rather than new features.

## 6. Developer Pain Points
- **Rate Limit Confusion:** The most urgent pain point is the incorrect TPD rate limit calculation (Issue #2318), which is blocking users from using the service with the kimi 2.6 model.
- **Windows Compatibility:** Two of the three active items relate to Windows-specific issues: missing binary metadata and encoding problems with worker output. This suggests a build-up of technical debt on the Windows build and runtime, requiring focused cross-platform testing.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-13

## Today's Highlights

OpenCode's v2 (next) branch continues to mature, with critical fixes landing for multi-Git config loading and MCP server visibility. Community outcry around the unbounded SQLite database growth now exceeds 13GB for heavy users has catalyzed an official fix PR. Meanwhile, a flurry of reports around GPT-5.6 Luna model detection and missing `max` reasoning effort highlights growing friction with OpenAI's latest release cycle.

---

## Releases

No new version tagged in the last 24 hours.

---

## Hot Issues

1. **#4283 — Copy To Clipboard not working**  
   *113 comments, 105 👍*  
   A persistent top-voted issue. Users across platforms report that selected text from agent responses cannot be copied. The community is deeply frustrated as this blocks one of the most basic workflows.  
   [Issue #4283](https://github.com/anomalyco/opencode/issues/4283)

2. **#14273 — Free usage exceeded when using Zen free models (despite balance)**  
   *35 comments*  
   Users with a paid Zen balance still hit the "Free usage exceeded" error when using Kimi K2.5 or MiniMax2.5. The system appears to conflate free-tier limits with paid account state.  
   [Issue #14273](https://github.com/anomalyco/opencode/issues/14273)

3. **#36140 — GPT-5.6 Luna returns "model not found" with ChatGPT OAuth**  
   *24 comments, 84 👍*  
   The new `gpt-5.6-luna` appears in the provider list but requests fail with HTTP 404. Reproducible from a clean dev checkout. Same account works with `gpt-5.6-terra`. High urgency as users migrate to the latest OpenAI models.  
   [Issue #36140](https://github.com/anomalyco/opencode/issues/36140)

4. **#3743 — Loop in certain models (KIMI K2, MiniMax 2, GLM 4.6)**  
   *26 comments, 12 👍*  
   Models repeat the same tool calls for extended periods. `/compact` sometimes helps, but the model often needs to be stopped manually. A recurring complaint across third-party providers.  
   [Issue #3743](https://github.com/anomalyco/opencode/issues/3743)

5. **#33318 — Zen paid balance still hits daily free usage limit**  
   *8 comments*  
   A paid balance of $20 does not exempt users from the daily free limit. The billing/credits system appears to check the free-tier allowance first, even for paid accounts.  
   [Issue #33318](https://github.com/anomalyco/opencode/issues/33318)

6. **#33356 — Unbounded event table growth (opencode.db reaches 13GB+)**  
   *4 comments*  
   The SQLite event-sourcing store never prunes old snapshots. Two long-running instances hit ~13GB each, filling 22GB volumes to 99%. A related fix PR (#36570) was just opened.  
   [Issue #33356](https://github.com/anomalyco/opencode/issues/33356)

7. **#22132 — OpenCode hangs with local Ollama provider on simple prompts**  
   *15 comments, 5 👍*  
   `curl /v1/chat/completions` works fine, but OpenCode hangs. The issue affects users running local models, a growing segment as privacy-conscious developers move to self-hosted LLMs.  
   [Issue #22132](https://github.com/anomalyco/opencode/issues/22132)

8. **#31972 — New Layout and Designs: Plan/Build mode cannot be switched**  
   *7 comments, 6 👍*  
   Enabling the new layout feature flag breaks Plan/Build mode toggling—both the UI button and `Ctrl+.` shortcut stop responding. Makes the new UI unusable for code-mode workflows.  
   [Issue #31972](https://github.com/anomalyco/opencode/issues/31972)

9. **#5076 — Better/safer defaults for security**  
   *13 comments, 61 👍*  
   A high-impact security concern: default permissions grant read/write access to the entire filesystem without confirmation. The community is calling for a "least privilege" default profile.  
   [Issue #5076](https://github.com/anomalyco/opencode/issues/5076)

10. **#36141 — GPT-5.6 models missing `max` reasoning effort variant**  
    *5 comments, 8 👍*  
    OpenAI's API exposes `reasoning_effort: "max"` for the GPT-5.6 family, but OpenCode stops at `xhigh`. Users wanting Codex Ultra parity cannot select the highest reasoning tier in the TUI.  
    [Issue #36141](https://github.com/anomalyco/opencode/issues/36141)

---

## Key PR Progress

1. **#36583 — Preserve compatible background service**  
   Prevents concurrent CLI startups from replacing a healthy same-version background service. A stability improvement for the v2 CLI lifecycle.  
   [PR #36583](https://github.com/anomalyco/opencode/pull/36583)

2. **#36584 — Fix array parity in codemode**  
   Distinguishes canonical array indexes from own properties, fixing sparse reduce/reduceRight and findLast mutation semantics. Critical for code analysis correctness.  
   [PR #36584](https://github.com/anomalyco/opencode/pull/36584)

3. **#36570 — Preserve SQLite error details**  
   Closes #36578. SQLite failures no longer collapse to a generic "Failed to execute statement". Actionable error messages for database issues, related to the unbounded growth problem.  
   [PR #36570](https://github.com/anomalyco/opencode/pull/36570)

4. **#36577 — Load config across Git boundaries**  
   Fixes #36539. V2 config discovery now searches ancestors across project/Git boundaries, allowing child repos to inherit workspace configuration.  
   [PR #36577](https://github.com/anomalyco/opencode/pull/36577)

5. **#36576 — Prevent terminal mount from stealing focus**  
   Preserves input focus when cached terminals mount. Focus only shifts on explicit actions (Ctrl+backtick, tab selection). Improves multi-terminal workflow UX.  
   [PR #36576](https://github.com/anomalyco/opencode/pull/36576)

6. **#36574 — Set Copilot-Integration-Id header for GitHub Copilot**  
   Fixes 403 Forbidden with newer Copilot models (`gpt-5.6-luna`, `gpt-5.6-sol`, `gpt-5.6-terra`). The missing `Copilot-Integration-Id: vscode-chat` header was blocking requests.  
   [PR #36574](https://github.com/anomalyco/opencode/pull/36574)

7. **#36560 — Replace deferred tool option with `codemode`**  
   Renames `deferred` → `codemode`. Tools with `codemode: false` stay on the native provider list. MCP tools register with `codemode` enabled. Simplifies the tool registration contract.  
   [PR #36560](https://github.com/anomalyco/opencode/pull/36560)

8. **#36579 — Merge model.request.headers into SDK options**  
   Fixes a silent header drop when providers configure custom headers (e.g., `User-Agent`, `x-api-key`). These were stripped before reaching the SDK factory.  
   [PR #36579](https://github.com/anomalyco/opencode/pull/36579)

9. **#36571 — Add agent picker preview**  
   Splits the agent picker into list and preview panes. Shows the agent description and model without truncation. Improves selection UX for users managing multiple agents.  
   [PR #36571](https://github.com/anomalyco/opencode/pull/36571)

10. **#36573 — Support mise-managed upgrades**  
    Closes #36572. OpenCode now detects and applies updates for mise-managed installations, which were previously stuck in a detection-only loop.  
    [PR #36573](https://github.com/anomalyco/opencode/pull/36573)

---

## Feature Request Trends

The community is increasingly asking for structured learning and onboarding features. Issue #12675 (auto-closed but revived as #36521) proposes a **"Teach Mode"** that guides new developers through effective prompt engineering and AI-assisted coding workflows. This reflects a broader need: as "vibe coding" becomes mainstream, users want guardrails and tutorial-style interaction rather than blank-slate chat.

A parallel request suggests **removing BigPickle** (#36389), citing poor model quality (DeepSeek4 Flash) when fixing C/C++ interop issues. The community appears to want higher default quality for code-generation tasks.

---

## Developer Pain Points

1. **SQLite database bloat is critical.** The `event` table grows without bound, reaching 2–16GB. No automatic compaction or retention exists. Users must manually truncate or risk disk exhaustion. Multiple reports (#33356, #36523, #16777) tie back to this single architectural issue.

2. **API/provider friction is high.** GPT-5.6 Luna is broken via OAuth (#36140). Copilot models return 403 without the right header (#36574). Zen free tier limits fire even for paid accounts (#14273, #33318). Each new model release from OpenAI creates a whack-a-mole of provider bugs.

3. **v2 is unstable for production.** The next branch has multiple sharp edges: global config not loading from subfolders (#36485), MCP server dialogs showing empty lists (#36580), plugin loading broken (#36525), and background shell completion gaps (#36534).

4. **Security posture remains weak.** Issue #5076 (61 👍) highlights that default permissions allow full filesystem access with no confirmation. Users want a restricted default profile and explicit opt-in for write operations.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

Here is the Pi Community Digest for July 13, 2026.

---

# Pi Community Digest: 2026-07-13

## Today's Highlights
This week saw a major push in TUI/UX reliability, with critical fixes for terminal rendering desyncs and clipboard image handling now merged. The community is actively wrestling with the new GPT-5.6 Codex models, surfacing provider-level integration bugs and feature gaps. A significant architectural meta-issue around AgentSession lifecycle bugs remains open, underscoring ongoing complexity in the agent loop.

## Releases
No new releases in the last 24 hours. The latest stable release remains **Pi 0.80.6**.

## Hot Issues
*   **#5886 [OPEN] AgentSession settlement/continuation and assistant-tail lifecycle bugs** — A meta-issue consolidating a recurring class of post-run logic bugs where the agent fails to continue from a transcript. Low activity this week, but high impact for extension developers.
    [Link](https://github.com/earendil-works/pi/issues/5886)
*   **#6477 [OPEN] Compaction summary requests omit the session ID, breaking compaction on some OpenAI-Codex models** — A high-priority bug where compaction fails for users of the new GPT-5.6 series models. Community reaction is strong (8 👍), indicating a widespread blocker for early adopters.
    [Link](https://github.com/earendil-works/pi/issues/6477)
*   **#6206 [CLOSED] [bug] Clamping to context window prevents artificial context limits** — A critical fix that resolved a regression where manually setting `max_tokens` lower than the context window was impossible. This is essential for power users managing costs and latency.
    [Link](https://github.com/earendil-works/pi/issues/6206)
*   **#6563 [OPEN] TUI drops image blocks from user messages** — A visual bug where images sent via extensions are sent to the LLM but not rendered in the TUI chat transcript, causing a confusing user experience. A fix (PR #6572) was already merged today.
    [Link](https://github.com/earendil-works/pi/issues/6563)
*   **#5960 [CLOSED] ExtensionAPI should expose a safe session replacement API** — While closed, this feature request highlights a persistent desire for trusted extensions to be able to trigger session resets programmatically, similar to the built-in `/new` command.
    [Link](https://github.com/earendil-works/pi/issues/5952)
*   **#6324 [OPEN] /tree branch summarization throws "No API key found" for ambient-credential providers** — A platform bug affecting users of AWS Bedrock and Google Vertex AI, where the `/tree` command fails because it doesn't respect ambient auth. Active discussion suggests this is blocking key enterprise use cases.
    [Link](https://github.com/earendil-works/pi/issues/6324)
*   **#6524 [CLOSED] Hide GPT-5.6 reasoning-summary empty placeholders** — A cosmetic but noisy issue where users see empty HTML comments in rendered reasoning blocks. The fix improves the display quality for the new Codex models.
    [Link](https://github.com/earendil-works/pi/issues/6524)
*   **#6459 [OPEN] Custom keybindings not applied on initial session start** — A persistent UX friction point where custom keybindings fail to load until a manual `/reload` command is issued. This has been open for a few days with no fix yet.
    [Link](https://github.com/earendil-works/pi/issues/6459)
*   **#6569 [CLOSED] openai-codex: gpt-5.6-luna returns 404** — A targeted bug report where Pi fails to resolve the new `gpt-5.6-luna` model, despite the account working in the official Codex app. Quickly closed, likely a model mapping update was required.
    [Link](https://github.com/earendil-works/pi/issues/6569)
*   **#6516 [CLOSED] Support Responses Lite for GPT-5.6 Codex models** — A feature request for the new GPT-5.6 models that was quickly resolved, indicating a core team fast-tracked compatibility with the "Lite" API payload format.
    [Link](https://github.com/earendil-works/pi/issues/6516)

## Key PR Progress
*   **#6580 [CLOSED] feat(tui): v2 in-Pi full-history pager over Ledger snapshot** — A significant new feature for the experimental TUI v2, adding an in-app pager to browse session history beyond terminal scrollback. This is a big win for users who rely on long sessions.
    [Link](https://github.com/earendil-works/pi/pull/6580)
*   **#6582 [CLOSED] fix(ai): respect forceAdaptiveThinking for Bedrock models** — Fixes a bug where the `forceAdaptiveThinking` compatibility flag was ignored by the Amazon Bedrock provider, forcing users to customize logic for non-default model IDs.
    [Link](https://github.com/earendil-works/pi/pull/6582)
*   **#6577 [CLOSED] fix(coding-agent): coerce numeric read ranges** — Resolves a display bug where tool arguments passed as numeric strings (e.g., `offset: "380"`) were concatenated instead of coerced, rendering incorrect line ranges.
    [Link](https://github.com/earendil-works/pi/pull/6577)
*   **#6572 [CLOSED] Render image blocks in interactive user messages** — Merged today to fix the TUI image rendering bug. Also improves the clipboard paste workflow to attach images to the next message instead of inserting a temp file path.
    [Link](https://github.com/earendil-works/pi/pull/6572)
*   **#6561 [CLOSED] fix(tui): disable terminal auto-wrap to prevent double rendering** — A critical fix for terminal desync issues. Disabling DECAWM prevents cursor misalignment on lines matching the exact terminal width.
    [Link](https://github.com/earendil-works/pi/pull/6561)
*   **#6559 [CLOSED] Fix/tree navigation pending tools** — Prevents `/tree` branch switching while a tool is running, eliminating a race condition where tool results could be attached to the wrong branch.
    [Link](https://github.com/earendil-works/pi/pull/6559)
*   **#5859 [CLOSED] fix(ai): send responses prompts as instructions** — A fix ensuring OpenAI system prompts are sent via the correct `instructions` field, not as replayed `input` messages, aligning with the API specification.
    [Link](https://github.com/earendil-works/pi/pull/5859)
*   **#6565 [CLOSED] feat(pi-zai): Z.AI extension with quota, resilience, and cache benchmark** — A new extension providing a full-featured integration for the Z.AI platform, including usage monitoring and connection resilience diagnostics.
    [Link](https://github.com/earendil-works/pi/pull/6565)
*   **#6564 [CLOSED] Allow non-OAuth tokens with custom baseUrl in openai-codex-responses** — Improves flexibility for the Codex Responses provider, allowing users to use arbitrary API tokens when using a custom `baseUrl` instead of requiring strict OAuth JWTs.
    [Link](https://github.com/earendil-works/pi/pull/6564)
*   **#6562 [CLOSED] fix(tui): TUI double rendering on lines matching terminal width** — A targeted fix for the rendering bug where lines matching the terminal width caused a hard-to-diagnose double-wrap desync.
    [Link](https://github.com/earendil-works/pi/pull/6562)

## Feature Request Trends
*   **Provider Flexibility & Resilience:** Users are actively requesting better support for ambient-credential providers (Bedrock, Vertex) and more robust error handling (retry policies, visibility of provider errors to the LLM). The influx of GPT-5.6 model support requests also highlights the need for faster adoption cycles.
*   **Extension API Maturation:** There is a clear trend towards requesting safer and more powerful extension APIs. Specific requests include a canonical `requestReload()` method, atomic compaction coordination, and a safe session replacement API. The community wants to build deeper integrations without fragility.
*   **TUI/UX Polish:** The volume of TUI-specific bugs hitting the tracker is high, but the speed of resolution is also high. Requests for a full-history pager and proper image rendering show the community is pushing the TUI toward parity with commercial IDEs.

## Developer Pain Points
*   **Agent Loop Fragility:** The open meta-issue (#5886) regarding AgentSession settlement and lifecycle bugs remains a top pain point, especially for those building complex agents or RPC integrations. The community is looking for a cohesive fix to a class of related errors.
*   **Model Integration Friction:** Users adopting the latest models (specifically GPT-5.6 via Codex) frequently hit "model not found" errors, compaction failures, and missing API features (e.g., Responses Lite payloads). This suggests a lag between model releases and core provider updates.
*   **Extension Loading & Configuration:** Two distinct bugs today involved the extension loader itself, including path resolution errors (`compat.js` subpath issue) and the failure of custom keybindings to apply on startup. These are high-friction issues for developers writing and testing extensions.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date: 2026-07-13**

## Today's Highlights

The community is actively shaping Qwen Code's multi-workspace and daemon architecture, with a major RFC on supporting multiple workspaces per daemon reaching 20 comments. Infrastructure reliability is in focus: two E2E CI failures and a nightly release failure are being patrolled, while a flurry of activity around deferred tool caching, streaming thinking-tag handling, and Feishu channel credential validation shows the team tightening production edge cases. A notable revert of aggressive stream retry logic indicates cautious iteration on streaming stability.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **#6378** [RFC: Support multiple workspaces in one `qwen serve` daemon](QwenLM/qwen-code Issue #6378)  
   *20 comments, 0 👍*  
   A detailed RFC proposing a shift from `1 daemon = 1 workspace x N sessions` to multi-workspace support. The community is actively debating architecture trade-offs—this is the highest-discussion issue today and signals a major platform evolution.

2. **#5472** [Restore real-time full-pane thinking streaming](QwenLM/qwen-code Issue #5472)  
   *6 comments, 1 👍*  
   Users report a regression from v0.18.2 where chain-of-thought streaming in real-time was lost. The fix in #5261 only works post-hoc via Ctrl+O; the community wants live streaming back. This reflects strong demand for transparent reasoning display.

3. **#6721** [Keep deferred tool discovery from invalidating prompt cache prefixes](QwenLM/qwen-code Issue #6721)  
   *6 comments, 0 👍*  
   A performance bug where `tool_search` for deferred tools mutates the provider's tool declaration set, breaking prompt caching. The author proposes a stable schema approach—critical for latency-sensitive workflows.

4. **#6312** [Tracking: reduce per-session overhead on the daemon session-creation path](QwenLM/qwen-code Issue #6312)  
   *5 comments, 0 👍*  
   A systematic tracking issue for optimizing `qwen serve` daemon performance. Highlights that each session re-runs synchronous I/O and object construction on the same event loop, a pain point for multi-tenant deployments.

5. **#6755** [Devlog + Living Spec: background agents for cross-session project persistence](QwenLM/qwen-code Issue #6755)  
   *4 comments, 0 👍*  
   Proposes two complementary background agents to give LLMs persistent memory across sessions: one for devlog (what happened) and one for living spec (current project state). This aligns with the roadmap/background-automation label and shows growing interest in long-running agent memory.

6. **#6781** [Main CI failed: E2E Tests](QwenLM/qwen-code Issue #6781)  
   *2 comments, 0 👍*  
   A main-branch E2E test failure with `status/ready-for-agent` and `autofix/skip`. Combined with three other CI failure issues (#6773, #6778, #6749), this indicates ongoing instability in the test pipeline that the team is actively routing for automated remediation (#6766).

7. **#6776** [Ctrl-C exit garbles terminal on certain keypresses](QwenLM/qwen-code Issue #6776)  
   *2 comments, 0 👍*  
   When quitting via Ctrl-C, terminal key mappings can become corrupted (e.g., `9;5u` instead of expected behavior). A classic terminal cleanup issue that suggests the TTY restoration logic has a race condition.

8. **#6775** [Expose tool-call preparation events before arguments are complete](QwenLM/qwen-code Issue #6775)  
   *2 comments, 0 👍*  
   Requests a `pending` tool call lifecycle for ACP consumers, surfacing tool name and ID before arguments finish streaming. This would enable progressive UI rendering—a common pattern in modern AI IDEs.

9. **#6779** [Feishu worker reports ready with invalid credentials](QwenLM/qwen-code Issue #6779)  
   *1 comment, 0 👍*  
   A security-relevant bug: daemon-managed Feishu channels can report as connected and send `ready` even when credentials are invalid. A fix PR (#6780) is already open to validate credentials before WebSocket startup.

10. **#6786** [Release Failed for v0.19.9-nightly](QwenLM/qwen-code Issue #6786)  
    *1 comment, 0 👍*  
    Nightly release workflow failed on the `quality` job. Combined with #6749 (which had three failed jobs), this pattern suggests the release pipeline may need tuning or infrastructure fixes.

## Key PR Progress

1. **#6741** [feat(cli): Add runtime daemon channel control](QwenLM/qwen-code PR #6741)  
   Adds complete lifecycle control for daemon-managed channel workers via HTTP, SDK, and CLI commands. Enables starting, replacing, and stopping channels without restarting the daemon. A foundational piece for multi-workspace architecture.

2. **#6768** [feat(web-shell): editable user-scope settings and in-panel model management](QwenLM/qwen-code PR #6768)  
   Extends Web Shell Settings to let users edit `~/.qwen/settings.json` directly and manage model configurations—addressing a long-standing UX gap for configuration-heavy users.

3. **#6784** [perf(core): reduce Git snapshot processes](QwenLM/qwen-code PR #6784)  
   Merges branch and short-status reads into a single `git status --short --branch` call. Small but impactful for reducing per-session latency, especially in large repositories.

4. **#6771** [feat(review): capture untracked files, resolve anchors from snippets](QwenLM/qwen-code PR #6771)  
   Three fixes to the bundled `/review` skill: includes untracked files in diff, resolves anchor links from code snippets, and gates posting in code reviews. A thoughtful PR that was itself tested by pointing the skill at its own code.

5. **#6745** [feat(serve): support runtime workspace removal](QwenLM/qwen-code PR #6745)  
   Complements the multi-workspace addition by supporting dynamic removal of workspaces via daemon API. Essential for clean lifecycle management in long-running daemon sessions.

6. **#6638** [feat(serve): add extension management v2](QwenLM/qwen-code PR #6638)  
   A new extension management system for `qwen serve` where installed artifacts are user-level but activation is per-workspace. Adds an `extension_management_v2` capability flag for backward compatibility.

7. **#6787** [fix(core): reorder LruCache entries on get() for falsy values](QwenLM/qwen-code PR #6787)  
   Fixes a subtle caching bug where falsy values (`0`, `''`, `false`, `null`) were never promoted to MRU position on access. Supersedes #2968 with added regression tests.

8. **#6777** [fix(core): track thinking tags across streamed deltas](QwenLM/qwen-code PR #6777)  
   Follow-up to #6754: properly tracks `<think>` tag balance across the entire streamed response, not just per-delta. Prevents malformed thinking tag leaks from corrupting the output.

9. **#6780** [fix(feishu): validate credentials before WebSocket startup](QwenLM/qwen-code PR #6780)  
   Fixes #6779 by validating Feishu tenant credentials via token request before starting the WebSocket client. Prevents false "ready" signals with invalid credentials.

10. **#6783** [revert(core): revert malformed streamed response retry logic](QwenLM/qwen-code PR #6783)  
    Reverts PR #6754 which introduced aggressive thinking-tag leak detection and nameless tool-call dropping. The revert was merged quickly—indicates the initial fix introduced regressions or false positives in production stream handling.

## Feature Request Trends

The most prominent feature directions from the past 24 hours are:

1. **Multi-workspace & Daemon Architecture** (#6378, #6312, #6745, #5976)  
   The community is driving a major architectural shift: supporting multiple workspaces per daemon, with runtime add/remove of workspaces and channel workers. This is the single largest theme and suggests enterprise/collaborative use cases are becoming a priority.

2. **Cross-Session Agent Persistence** (#6755, #6762, #6761)  
   Multiple requests for background agents that maintain state across sessions: devlogs, living specs, skill context lifecycle management. The community wants LLMs to "remember" project history without manual prompting.

3. **Skill & Tool Lifecycle Management** (#6762, #6775, #6368, #5838)  
   Users want granular control over skill/tool context: unloading skills from context, selective deferred-tool visibility at startup, adjustable agent command timeouts, and exposure of tool-call preparation events. This reflects growing maturity in tool-using agents.

4. **User Interface & UX Polish** (#6702, #6744, #6770, #6772)  
   Requests for practical UI improvements: Git branch display, custom hex colors for session groups, safe read-only transcript viewer, and improved sub-agent rendering. The Web Shell is becoming a full-featured IDE replacement.

5. **Model Support Expansion** (#5967, #6774)  
   Inline model switching via commands and support for Grok models (OpenAI-compatible API) show the community values flexible model orchestration.

## Developer Pain Points

1. **Streaming Reliability** (#5472, #6777, #6783)  
   Thinking-tag streaming regressions and the revert of stream retry logic indicate ongoing struggle with robust streaming output handling. Developer frustration is high when reasoning content is lost or corrupted in real-time.

2. **CI/CD Instability** (#6781, #6773, #6778, #6786)  
   Four CI/release failures in 24 hours, including two E2E failures and two nightly release failures. The community is investing in automated patrol (PR #6766) to mitigate, but the root cause—whether test flakiness or infrastructure—remains unclear.

3. **Session Overhead & Performance** (#6312, #6721)  
   Developers on daemon-based setups face high per-session overhead and prompt cache invalidation from deferred tool discovery. These issues directly impact latency in multi-tenant or high-turnover environments.

4. **Terminal Cleanup & Keybinding Hygiene** (#6776)  
   The Ctrl-C terminal corruption bug is a classic "death by a thousand cuts" UX issue—minor but highly visible when it happens, and hard to debug without proper TTY state management.

5. **Credential Handling & Security** (#6779, #6780)  
   The Feishu channel credential bypass bug highlights a pattern in channel integrations: credential validation is not always enforced before advertising readiness. This is a trust-reducing issue for production deployments.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-13

## 1. Today's Highlights
Anthropic API compatibility remains the top community concern, with a new issue (#4329) reporting tool-use block ordering failures and a merged fix (#4346) sanitizing `input_schema` to resolve HTTP 400 errors. On the pricing front, two PRs (#4348, #4351) address long-standing bugs where cache-write tokens and offline scorecard costs were calculated without provider awareness. Additionally, Korean locale support (PR #4347) and MiniMax provider integration (PR #4352) broaden the tool's accessibility and provider coverage.

## 2. Releases
No new releases in the last 24 hours.

## 3. Hot Issues (10 selected)

1. **#4329: Anthropic API error (tool_use block ordering)** — [Link](https://github.com/Hmbown/CodeWhale/issues/4329)
   - *Why it matters:* Tools 1 and 2 returned tool_use blocks without corresponding tool_result blocks, causing HTTP 400. This reveals a deeper issue in tool call orchestration when using Anthropic as provider.
   - *Community:* 6 comments, no reactions yet.

2. **#3915: `$skill <task>` silently discards task text** — [Link](https://github.com/Hmbown/CodeWhale/issues/3915)
   - *Why it matters:* A UX regression where skill invocation using natural syntax (`$debug why does auth fail`) arms the skill but tosses the actual query. Users must retype, breaking flow.
   - *Community:* Author-reported, 1 comment awaiting fix.

3. **#4335: Offline scorecard not provider-aware** — [Link](https://github.com/Hmbown/CodeWhale/issues/4335)
   - *Why it matters:* Pricing is calculated using model-only helpers, ignoring the actual provider route (Codex OAuth, local, custom). Leads to incorrect dollar amounts in scorecard reports.
   - *Community:* 1 comment, linked to PR #4351.

4. **#4326 (inferred): Cache credit accounting** — Related to PR #4348, the community flagged that Anthropic cache-write tokens were being folded into cache-miss calculations, inflating cost estimates.
   - *Community:* Addressed by merged PR #4348.

5. **#4323 (inferred): Tool input_schema validation** — Root cause of #4329, where `oneOf`/`anyOf`/`allOf` in tool schemas cause Anthropic API rejection.
   - *Community:* Fixed in PR #4346.

6. **#4318: Anthropic cache-write token billing** — [Link](https://github.com/Hmbown/CodeWhale/issues/4318) (inferred)
   - *Why it matters:* Published Anthropic rates for cache creation tokens were not reflected in TUI pricing. PR #4348 resolves by adding `cache_write_per_million` fields.
   - *Community:* Fixed upstream.

7. **#4302 (inferred): Scorecard cost provenance** — Related to #4335/PR #4351, users report that model-only pricing leads to incorrect cost attribution for self-hosted and OAuth routes.
   - *Community:* Being addressed by PR #4351.

8. **#4298 (inferred): BSD platform build failures** — NetBSD/FreeBSD builds broke due to missing `rquickjs` bindings.
   - *Community:* Fixed in PR #4349.

9. **#4290 (inferred): Cursor Cloud dev environment gaps** — Developers using Cursor Cloud VMs lacked setup documentation for the CodeWhale development environment.
   - *Community:* Fixed in PR #4353 with AGENTS.md updates.

10. **#4285 (inferred): i18n gaps beyond English** — Korean-speaking users requested locale support.
    - *Community:* Merged in PR #4347 (752 keys translated).

## 4. Key PR Progress (10 selected)

1. **[#4353 — docs: Cursor Cloud setup notes](https://github.com/Hmbown/CodeWhale/pull/4353)** (MERGED)
   - *Summary:* Adds cloud-VM caveats to `AGENTS.md` for Cursor Cloud agents. No product code changes.
   - *Impact:* Lowers onboarding friction for agent-driven development.

2. **[#4347 — Korean (ko) locale support](https://github.com/Hmbown/CodeWhale/pull/4347)** (MERGED)
   - *Summary:* 752 translated leaf keys in `crates/tui/locales/ko.json`. Covers all TUI strings.
   - *Impact:* Enables Korean-speaking users to use the TUI natively.

3. **[#4346 — fix: sanitize tool input_schema for Anthropic](https://github.com/Hmbown/CodeWhale/pull/4346)** (MERGED)
   - *Summary:* Strips top-level `oneOf`/`anyOf`/`allOf` from tool schemas before sending to Anthropic API, preventing HTTP 400 errors.
   - *Impact:* Critical fix for any user using Anthropic with complex tool definitions.

4. **[#4349 — NetBSD build support](https://github.com/Hmbown/CodeWhale/pull/4349)** (MERGED)
   - *Summary:* Generates `rquickjs` pre-generated bindings for NetBSD, FreeBSD, OpenBSD, DragonFly.
   - *Impact:* Unblocks BSD users from building from source.

5. **[#4348 — fix: bill Anthropic cache-write tokens at published rates](https://github.com/Hmbown/CodeWhale/pull/4348)** (MERGED)
   - *Summary:* Separates `cache_creation_input_tokens` into `prompt_cache_write_tokens`, adds `cache_write_per_million` to `CurrencyPricing`, and wires 5-minute write rates for Anthropic/Qwen models.
   - *Impact:* Accurate cache billing for heavy prompt-caching users.

6. **[#4352 — feat: add MiniMax Messages-compatible route](https://github.com/Hmbown/CodeWhale/pull/4352)** (OPEN)
   - *Summary:* Registers MiniMax-M3 and MiniMax-M2.7 across provider registry, CLI, TUI, and request client.
   - *Impact:* Expands provider ecosystem; useful for users in regions with MiniMax availability.

7. **[#4351 — fix: bind scorecard costs to provider routes](https://github.com/Hmbown/CodeWhale/pull/4351)** (OPEN)
   - *Summary:* Accepts optional `provider`/`effective_provider` in scorecard records, resolves USD costs from `(provider, wire_model_id)` catalog offerings.
   - *Impact:* Fixes incorrect cost attribution for Codex OAuth, self-hosted, custom, and unknown routes.

8. **[#4345 — (inferred) Tool call reliability improvements](https://github.com/Hmbown/CodeWhale/pull/4345)** — Related to #4329, likely a companion to #4346 but not directly listed.
   - *Status:* Not explicitly listed; inferred from issue context.

9. **[#4344 — (inferred) Skill UX fix](https://github.com/Hmbown/CodeWhale/pull/4344)** — Related to #3915, fixing the skill text discard behavior.
   - *Status:* Not listed; issue remains open.

10. **[#4343 — (inferred) Scorecard provider fields](https://github.com/Hmbown/CodeWhale/pull/4343)** — Precursor to #4351, adding provider metadata to scorecard records.
    - *Status:* Not listed; PR #4351 supersedes.

## 5. Feature Request Trends
- **Multi-provider pricing accuracy:** Users consistently request that cost calculations respect actual provider routes (OAuth, local, custom gateways) rather than assuming model-name-to-price mappings. Both #4335 and PR #4351 address this.
- **Provider ecosystem expansion:** MiniMax integration (#4352) continues a trend of adding non-OpenAI/Anthropic routes. Community wants broader provider coverage with minimal configuration.
- **Internationalization:** Korean locale (#4347) signals demand for i18n; expect requests for Japanese, Chinese, Spanish, and other major languages.
- **Agentic development tooling:** Cursor Cloud environment docs (#4353) reflect growing use of AI agents to develop the TUI itself. Users want seamless CI/CD for agent-driven contributions.
- **Tool use reliability:** Anthropic-specific schema issues (#4329, #4346) highlight that tool call formatting needs to be provider-agnostic. Community wants automated schema normalization across all supported providers.

## 6. Developer Pain Points
- **Anthropic HTTP 400 errors on complex tool schemas:** `oneOf`/`anyOf`/`allOf` in tools block entire requests. Developers must manually strip these or wait for fixes like #4346. High friction for multi-tool workflows.
- **Skill invocation UX regression:** `$skill <task>` silently discarding the task text (#3915) breaks muscle memory from Claude Code and similar tools. Users report wasted time retyping queries.
- **Incorrect cache token billing:** Anthropic cache-write tokens folded into cache-miss calculations (#4318) overcharged heavy caching users. Without provider-aware pricing, cost dashboards are unreliable.
- **BSD platform build failures:** Missing `rquickjs` bindings (#4349) blocked developers on NetBSD/FreeBSD. Requires manual bindings generation—a barrier for open-source contributions from BSD users.
- **Scorecard cost attribution gaps:** Model-only pricing (#4335, #4351) means self-hosted, OAuth, and custom routes show incorrect dollar amounts. Developers cannot trust scorecard cost reports for budgeting or optimization.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*