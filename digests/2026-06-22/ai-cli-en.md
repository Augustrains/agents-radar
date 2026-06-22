# AI CLI Tools Community Digest 2026-06-22

> Generated: 2026-06-22 02:30 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem — Cross-Tool Comparison Report
**Date: 2026-06-22**

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with seven major projects now competing for developer mindshare. Today's data reveals a bifurcated ecosystem: established tools (Claude Code, OpenAI Codex, Gemini CLI) are struggling with API reliability and scaling pains, while newer entrants (Qwen Code, CodeWhale/DeepSeek TUI) iterate aggressively on feature velocity. A universal pattern emerges—every tool community is demanding better session persistence, memory/context management, and multi-provider flexibility. The most acute pain point across the board is **API instability and rate-limiting unpredictability**, which suggests upstream infrastructure is struggling to keep pace with adoption. Windows support remains a consistent weakness, with all tools showing platform-specific bugs that lag behind macOS/Linux parity.

---

## 2. Activity Comparison

| Metric | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code CLI | OpenCode | Pi | Qwen Code | CodeWhale (DeepSeek TUI) |
|---|---|---|---|---|---|---|---|---|---|
| **Hot Issues (24h)** | 10 | 10 | 10 | 8 | 10 | 10 | 10 | 10 | 10 |
| **Total Issue Comments (approx.)** | ~195 | ~347 | ~70 | ~12 | ~40 | ~120 | ~165 | ~45 | ~94 |
| **PRs Active (24h)** | 2 | 10 | 10 | 1 | 0 | 10 | 10 | 10 | 10 |
| **New Releases (24h)** | 0 | 3 (alpha) | 0 | 0 | 0 | 0 | 0 | 2 (stable + nightly) | 1 (v0.8.63) |
| **Top Issue Reactions (👍)** | 601 | 197 | N/A | 1 | 0 | 37 | 36 | 0 | 0 |
| **Community Engagement Level** | Very High | High | Medium | Low | Low | Medium | High | Medium | Medium-High |

**Key observations:**
- **OpenAI Codex** leads raw issue volume (347+ comments) driven by the rate-limit cost regression (#28879 with 190 👍)
- **Claude Code** has the highest-engagement single issue (multi-account switching, 601 👍) but lower overall PR velocity
- **Gemini CLI** shows strong PR output (10 PRs) but lower community volume—suggesting more internal/team-driven development
- **GitHub Copilot CLI** has the lowest activity across all metrics, with only 12 total comments and 1 PR
- **Pi** and **OpenCode** show healthy community engagement relative to their maturity

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating genuine market demand:

### Session Persistence & Memory Management
| Requirement | Tools Requesting | Specific Needs |
|---|---|---|
| **Persistent cross-session context/memory** | Kimi Code (#1283), Pi (#3357), Gemini CLI (#26525), OpenCode (#14292) | AI-managed notes, project-specific memory, auto-summarization |
| **Session context window visibility** | Copilot CLI (#3867), Codex (#21128), Claude Code (implied) | Token usage counters, compaction notifications |
| **Session branching/forking** | Claude Code (#69272), Codex (implied) | `/fork` parity between CLI and IDE extensions |

### Multi-Account & Multi-Provider Management
| Requirement | Tools Requesting | Specific Needs |
|---|---|---|
| **Multi-account/profile switching** | Claude Code (#18435, 601👍), Gemini CLI (implied), CodeWhale (implied) | Consultant/team use cases, separate billing |
| **Model-specific configuration overrides** | Pi (#5933), OpenCode (#29354), CodeWhale (#3222) | Per-model limits, thinking levels, truncation |
| **Custom model provider support** | Pi (#5916), CodeWhale (#3357), Qwen Code (#5559) | OpenRouter config, local LLMs, custom endpoints |

### IDE Integration & UX Parity
| Requirement | Tools Requesting | Specific Needs |
|---|---|---|
| **IDE-integrated diff/approval** | Codex (#2998, 197👍), Claude Code (VSCode vs CLI gap) | Red/green diffs inside IDE panels |
| **Native IDE panels (IntelliJ/Android Studio)** | Claude Code (#69778), Kimi Code (implied) | Beyond terminal-only integration |
| **Context preservation across IDE restarts** | OpenCode (#32747), Codex (#21128) | File indexing, conversation history |

### Security & Governance
| Requirement | Tools Requesting | Specific Needs |
|---|---|---|
| **Pre-execution review gates** | Claude Code (#65982), CodeWhale (#3144), Pi (#5939) | Fact-check hooks, auto-review policies |
| **Hook/tool visibility & management** | Copilot CLI (#3871), Gemini CLI (implied) | List installed hooks, audit tool usage |
| **Sandbox network filtering** | Copilot CLI (#3861), Gemini CLI (implied) | Consistent isolation, documented behavior |

### Cross-Platform Reliability
| Requirement | Tools Requesting | Specific Needs |
|---|---|---|
| **Windows standalone installer** | Codex (#13993, 153👍), Kimi Code (#2432) | Corporate/offline, non-Microsoft Store |
| **Windows ARM64 stability** | Copilot CLI (#3687), Qwen Code (#5538) | Crash fixes, UNC path handling |
| **WSL agent mode** | Codex (#16815), OpenCode (#22223) | Serialization fixes, display compatibility |

---

## 4. Differentiation Analysis

### Feature Focus Differences

| Tool | Primary Differentiator | Target User | Technical Approach |
|---|---|---|---|
| **Claude Code** | Deep reasoning (Opus 1M context), rich agentic workflows | Professional developers, high-complexity projects | Python-based, heavy MCP ecosystem |
| **OpenAI Codex** | Tight GPT-5.5 integration, rate-limited "Plus" model | Individual developers, budget-conscious | Rust CLI, sandbox tooling, ACP protocol |
| **Gemini CLI** | Google Cloud integration, multi-model eval infrastructure | GCP-native teams, enterprise | Node.js/TypeScript, skill-based agents |
| **GitHub Copilot CLI** | GitHub ecosystem lock-in, sandbox isolation | GitHub-heavy workflows | Node.js, hook-based extensibility |
| **Kimi Code CLI** | MoonshotAI API, ACP pipeline mode | Automated CI/CD, pipeline developers | Go-based (likely), minimal docs today |
| **OpenCode** | Zen provider, YOLO mode, web client | Power users wanting flexibility | TypeScript, TUI + web, skill plugins |
| **Pi** | Local LLM first-class, OpenRouter support | Privacy-conscious, cost-sensitive | Rust, extension API, vLLM/llama.cpp |
| **Qwen Code** | QwenLM ecosystem, background sub-agents, voice dictation | Multimodal workflow enthusiasts | TypeScript, artifact tool, nightly releases |
| **CodeWhale (DeepSeek TUI)** | Rebranded DeepSeek TUI, WeCom integration, Chinese enterprise | Chinese enterprise, global open-source | Rust, sandbox, config monolith |

### Technical Architecture Divergence

- **Compaction strategies**: Pi is moving to opt-in auto-compaction at safe checkpoints (#5937); Codex is consolidating thread-store SQLite (#29355); Gemini CLI has JSONL-based sessions with repair logic
- **Agent orchestration**: Qwen Code emphasizes background sub-agents with TTL cleanup (#5556); CodeWhale spawns plan-mode sub-agents but suffers UI freezes (#3289); Claude Code pushes session-as-process primitive (#68996)
- **MCP integration maturity**: Codex just added MCP sandbox state consumption (#29358); CodeWhale splits MCP headers (#3333); Kimi Code's MCP tools are broken in ACP mode (#2464)—integration quality varies wildly

---

## 5. Community Momentum & Maturity

### Tier 1: Established & High-Community (Mature but strained)
- **Claude Code** — Largest community by engagement (601👍 on a single issue). API reliability issues suggest scaling challenges. Mature feature set but slower iteration.
- **OpenAI Codex** — Very high issue volume (347+ comments). Rate-limit crisis (#28879) is a trust emergency. Rapid alpha releases (3 in 24h) indicate active internal firefighting.

### Tier 2: Rapidly Iterating (High velocity, growing community)
- **Gemini CLI** — Strong PR output (10 PRs) with session recovery fixes. Community is smaller but vocal about memory system and evaluation infrastructure.
- **Pi** — Over 2 dozen issues closed in 24h. Strong focus on local LLM integration and extension API. Community is engaged (30👍 top issue).
- **CodeWhale (DeepSeek TUI)** — High PR velocity (10 PRs + rebranding release). Architectural refactoring signals a tool maturing past its initial identity.
- **OpenCode** — Steady PR flow (10 PRs) with ACP improvements. Community rallying around UX issues (37👍 on Ctrl+C).

### Tier 3: Emerging (Lower community, early adoption)
- **Qwen Code** — Active development (stable + nightly releases) but smaller community engagement. Voice dictation and artifact tool suggest unique multimodal ambitions.
- **Kimi Code CLI** — Low community activity (0 PRs, minimal comments). Persistent memory feature (#1283) is the strongest signal of latent demand.
- **GitHub Copilot CLI** — Lowest activity across all metrics. Windows ARM64 crash (#3687) and billing confusion (#3881) suggest a tool in maintenance mode.

---

## 6. Trend Signals — What Developers Should Watch

### 🔴 Critical (Immediate action needed for users of affected tools)

1. **Rate-limit unpredictability is a systemic risk** — OpenAI Codex's 10-20x cost regression (#28879) and Claude Code's API overload errors (#69942, #69945) suggest upstream inference capacity is strained. Developers should budget for intermittent availability issues and consider fallback providers.
2. **Windows remains a second-class platform** — Every tool except Pi has significant Windows-specific bugs. If your team deploys on Windows, expect extra friction with sandbox, path handling, and installer gaps.
3. **Security hooks are unreliable** — Copilot CLI's `preToolUse` denial is silently ignored (#3874); Claude Code's sandbox blocks legitimate Git workflows (#3355). Trust but verify your tool's security model.

### 🟡 Emerging (Trending across multiple communities)

4. **Local LLM integration is becoming table stakes** — Pi (#3357, 36👍), Qwen Code (#5559), and CodeWhale (#3222) all invest in local inference. Expect this to become a standard requirement within 6 months.
5. **Session-as-process primitives** — Claude Code (#68996) and Codex (#29357, #29367) are both building programmatic session control. This enables CI/CD integration and complex multi-session orchestration.
6. **Memory systems are the new "killer feature"** — Kimi Code (#1283), Gemini CLI (#26525), and OpenCode (#14292) all pursue persistent memory. Tools that solve this well will gain significant advantage.

### 🟢 Mature (Well-understood, stable implementations)

7. **MCP protocol adoption is accelerating but fragmented** — Codex (#29358), OpenCode (#29355), and CodeWhale (#3333) all extend MCP. However, Kimi Code's ACP mode breaks MCP entirely (#2464), and Copilot CLI has no MCP tools at all. Expect standardization pressure.
8. **Agent autonomy vs. safety tension** — Every tool reports agents being either too aggressive (destructive git/DB commands) or too passive (not using configured skills). The balance remains unsolved.
9. **Compaction is moving from opaque to observable** — Pi (#5939, #5941) and Codex (#29356) are making compaction behavior explicit with event metadata and user controls. This is a UX win that other tools should replicate.

### Recommendation for Technical Decision-Makers

- **Choose Claude Code or OpenAI Codex** for maximum capability and community support, but **budget for API instability** and monitor rate-limit announcements closely.
- **Choose Pi** if local LLM support and cost control are priorities; its extension API and compaction reliability work show maturity beyond its community size.
- **Choose CodeWhale** if you need Chinese enterprise integration (WeCom) and can tolerate architectural churn during rebranding.
- **Avoid GitHub Copilot CLI and Kimi Code CLI** for production use today—community activity and bug fix velocity are too low to trust for critical workflows.
- **Watch Qwen Code** for multimodal innovation (voice, artifacts) but treat it as experimental until background sub-agents stabilize.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** 2026-06-22 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following Skills generated the most community discussion through Pull Request activity:

### #1: Document Typography Skill (#514)
- **Skill:** Typographic quality control for AI-generated documents — prevents orphan word wrap, widow paragraphs, and numbering misalignment.
- **Discussion:** High engagement on the practical value proposition; users noted these issues affect "every document Claude generates." Some debate on whether typography rules should be built into the base model rather than a Skill.
- **Status:** Open | [PR #514](https://github.com/anthropics/skills/pull/514)

### #2: ODT Skill — OpenDocument Support (#486)
- **Skill:** Create, fill, read, and convert OpenDocument Format files (.odt, .ods) with template filling and ODT-to-HTML parsing.
- **Discussion:** Strong demand from enterprise users and open-source advocates. Discussion centered on compatibility with LibreOffice workflows and ISO standard compliance.
- **Status:** Open | [PR #486](https://github.com/anthropics/skills/pull/486)

### #3: Frontend-Design Skill Clarity Improvements (#210)
- **Skill:** Revises the existing frontend-design skill for better actionability, ensuring instructions are specific enough for Claude to follow in a single conversation.
- **Discussion:** Community members shared specific examples where the original skill produced vague output. The PR became a model for how to refactor existing Skills for precision.
- **Status:** Open | [PR #210](https://github.com/anthropics/skills/pull/210)

### #4: Skill-Creator Fixes — run_eval.py Recall Bug (#1298)
- **Skill:** Fixes the critical bug where `run_eval.py` reports 0% recall for every skill description, breaking the optimization pipeline.
- **Discussion:** The most technically intensive discussion. Links to Issue #556 (10+ independent reproductions). Generated debate about Windows compatibility, subprocess handling, and testing methodology.
- **Status:** Open | [PR #1298](https://github.com/anthropics/skills/pull/1298)

### #5: Skill-Quality and Skill-Security Analyzers (#83)
- **Skill:** Two meta-skills for evaluating other Skills across five quality dimensions (structure, documentation, completeness, compatibility, examples) and security analysis.
- **Discussion:** Early proposal for Skill governance. Community split on whether meta-skills should live in the marketplace or be tooling. Long-lived PR (since Nov 2025) still active.
- **Status:** Open | [PR #83](https://github.com/anthropics/skills/pull/83)

### #6: SAP-RPT-1-OSS Predictive Skill (#181)
- **Skill:** Interfaces with SAP's open-source tabular foundation model for predictive analytics on enterprise business data.
- **Discussion:** Enterprise-focused, generated interest from SAP ecosystem developers. Technical discussion on model integration patterns.
- **Status:** Open | [PR #181](https://github.com/anthropics/skills/pull/181)

### #7: Testing Patterns Skill (#723)
- **Skill:** Comprehensive testing coverage across the Testing Trophy model — unit tests, React component tests, integration, E2E, visual regression, and accessibility testing.
- **Discussion:** Broadly welcomed as filling a major gap in the collection. Discussion focused on whether to include specific framework examples or remain framework-agnostic.
- **Status:** Open | [PR #723](https://github.com/anthropics/skills/pull/723)

---

## 2. Community Demand Trends

From Issue activity, the community's most-anticipated directions are:

### 🏢 Enterprise & Organizational Features
- **Org-wide skill sharing (#228):** 14 comments, 7 upvotes. Users want direct sharing mechanisms within Claude.ai instead of manual `.skill` file distribution. *Highest-engagement issue overall.*
- **Security and trust boundary concerns (#492):** Community skills distributed under `anthropic/` namespace raise impersonation risks. Demand for verified/official badges and namespace governance.

### 🛠️ Tooling Reliability
- **Skill-Creator pipeline broken on Windows (#556, #1061, #1169):** The `run_eval.py` → `improve_description.py` optimization loop is non-functional for many users. Three separate issues tracking subprocess, encoding, and PATHEXT failures. This is the #1 blocker for Skill development.
- **Duplicate skill installations (#189):** Plugin system causes identical skills to load twice. 9 upvotes — the most-voted issue.

### 🔒 Security & Governance
- **Agent governance patterns (#412):** Proposal for safety patterns in AI agent systems — policy enforcement, threat detection, and audit trails. No existing Skill covers this domain.

### 📄 Document Handling
- **SharePoint Online document handling (#1175):** Security/context window concerns for enterprise document workflows.
- **Expose Skills as MCPs (#16):** Community wants Skills to expose a typed API surface through the Model Context Protocol.

---

## 3. High-Potential Pending Skills

These actively-discussed PRs are not yet merged but show strong community interest and technical readiness:

| PR | Skill | Relevance |
|----|-------|-----------|
| [#514](https://github.com/anthropics/skills/pull/514) | Document Typography | Universal value; addresses a pain point in every Claude output |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT OpenDocument | Enterprise compliance workflows |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing Patterns | Fills an obvious domain gap in the collection |
| [#568](https://github.com/anthropics/skills/pull/568) | ServiceNow Platform | Broad enterprise platform coverage (ITSM, ITOM, SecOps) |
| [#444](https://github.com/anthropics/skills/pull/444) | AURELION Skill Suite | Cognitive framework + memory for professional knowledge management |
| [#154](https://github.com/anthropics/skills/pull/154) | Shodh Memory | Persistent context across conversations; high demand for agent memory |

**Skill-Creator fixes** (#1298, #1099, #1050, #539, #541, #361, #362) are also high-priority — they unblock the entire Skill development pipeline, especially on Windows.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable, enterprise-grade Skill tooling and cross-session persistent memory**, rather than narrow domain-specific Skills — users are prioritizing fixing the development pipeline (Windows compatibility, evaluation accuracy) and enabling organizational sharing before expanding the Skill catalog.

---

# Claude Code Community Digest — 2026-06-22

## Today’s Highlights

API reliability issues dominate the community this week, with multiple reports of "Service Unavailable" (Opus), 502 errors, and 529 overloaded errors surfacing across platforms—suggesting upstream Anthropic API strain. A model-switching bug silently downgrades users from 1M Opus mid-session, causing unrecoverable errors. On the feature front, the community continues to push for multi-account management (118 comments, 601 👍), isolated session spawning, and fact-check gates at response-commit time.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (Top 10 by Community Impact)

1. **#18435 — Multi-account switching in Claude Desktop**  
   *[enhancement, area:auth, area:ide]*  
   The highest-engagement issue ever (118 comments, 601 👍). Users want profile-based account switching within the Desktop app—critical for consultants and teams managing multiple Anthropic accounts.  
   [GitHub](https://github.com/anthropics/claude-code/issues/18435)

2. **#36179 — `redacted_thinking` content type errors on Windows/VSCode**  
   *[bug, platform:windows, area:api, platform:vscode]*  
   Persistent errors break plugin usage on Windows. The `redacted_thinking` content type is not handled, causing silent failures. 29 comments, indicates a widespread Windows-specific API compatibility gap.  
   [GitHub](https://github.com/anthropics/claude-code/issues/36179)

3. **#69942 — "Service Unavailable" API error (macOS + VSCode)**  
   *[bug, platform:macos, external, area:api, platform:vscode]*  
   New today, 5 comments, 11 👍. Users across platforms report Anthropic API being down. Correlates with multiple concurrent reports of 502 and 529 errors.  
   [GitHub](https://github.com/anthropics/claude-code/issues/69942)

4. **#52765 — "Server is busy" error in Cowork Desktop on Windows**  
   *[bug, platform:windows, area:auth, area:cowork]*  
   Cowork sessions blocked by server-busy errors. 14 comments, indicates a systemic issue with Cowork session establishment on Windows.  
   [GitHub](https://github.com/anthropics/claude-code/issues/52765)

5. **#37994 — Desktop update breaks LAN SSH/network access (macOS)**  
   *[bug, platform:macos, area:networking, area:sandbox]*  
   `OPERON_SANDBOXED_NETWORK=1` enforcement blocks local network access after a March 23 update. SSH and curl to LAN hosts fail, breaking local dev workflows. 11 comments.  
   [GitHub](https://github.com/anthropics/claude-code/issues/37994)

6. **#69772 — Model silently switches from 1M to non-1M Opus mid-session**  
   *[bug, has repro, platform:macos, area:model]*  
   Critical bug: model downgrade triggers unrecoverable "API Error" without user notice. Session must be killed. `--resume` fails. 5 comments, 2 👍.  
   [GitHub](https://github.com/anthropics/claude-code/issues/69772)

7. **#54461 — Desktop app: cannot change working directory or open new chat (Windows)**  
   *[bug, platform:windows, area:desktop]*  
   Core functionality broken on Windows Desktop app. 8 comments.  
   [GitHub](https://github.com/anthropics/claude-code/issues/54461)

8. **#61912 — OAuth refresh corrupts credentials during transient 5xx → persistent 401 loop**  
   *[bug, has repro, platform:linux, area:auth]*  
   Transient Cloudflare 5xx errors during OAuth refresh permanently corrupt credentials, causing 401 loops across sessions. Requires logout/re-login. 5 comments.  
   [GitHub](https://github.com/anthropics/claude-code/issues/61912)

9. **#69807 — Cowork/Code sessions hang on load after Desktop update (macOS 26.5.1)**  
   *[bug, platform:macos, area:mcp, area:cowork, area:desktop]*  
   Desktop 1.14271.0 update introduced session hang on load. 3 comments, likely MCP-related regression.  
   [GitHub](https://github.com/anthropics/claude-code/issues/69807)

10. **#69945 — 529 Overloaded error (macOS + VSCode)**  
    *[bug, duplicate, platform:macos, external, platform:vscode, api:anthropic]*  
    5 👍 in first hours. Anthropic API overload—appears to be a broader capacity issue.  
    [GitHub](https://github.com/anthropics/claude-code/issues/69945)

---

## Key PR Progress

1. **#69916 — Fix silent exit in edit-issue-labels.sh**  
   Script fix for the Claude Issue Triage workflow. Prevents silent `exit 1` when no label arguments provided.  
   [GitHub](https://github.com/anthropics/claude-code/pull/69916)

2. **#4943 — Add shell completions (bash, zsh, fish)**  
   Long-running PR (since Aug 2025, still open). Adds static completion scripts for tab autocompletion of Claude CLI commands.  
   [GitHub](https://github.com/anthropics/claude-code/pull/4943)

---

## Feature Request Trends

- **Multi-account/profile management (#18435)** — Dominant request across Desktop and CLI. 601 👍, 118 comments.
- **Session-as-process primitive (#68996)** — Developers want programmatic spawning, communication, and termination of isolated Claude sessions from within a running session.
- **Fact-check gate at response-commit time (#65982)** — Users demand verification hooks that run before model output containing factual claims is committed.
- **Conversation branching/fork in VSCode (#69272)** — CLI supports `/fork`; VSCode extension does not. Developers want parity.
- **Native agent UI for IntelliJ/Android Studio (#69778)** — Terminal-based integration isn't enough; users want a native panel like VSCode's.
- **Rich text hyperlink preservation (#69948)** — URLs in rich text pastes are silently dropped—loss of context when pasting from docs/emails.
- **Customizable permission mode cycling (#32604, closed)** — Users want `dontAsk` included in the Shift+Tab cycle, not just set via config.
- **Linux/riscv64 native binary (#59813)** — Edge platform request, 3 comments, relevant for open hardware community.

---

## Developer Pain Points

| Pain Point | Symptoms | Frequency |
|---|---|---|
| **API instability** | 502, 529, "Service Unavailable" errors across platforms | High (3+ new issues today) |
| **Model mid-session downgrade** | Opus 1M silently switched to non-1M; unrecoverable | Medium |
| **Windows Desktop broken core** | Cannot change directory, open new chat, or establish Cowork | Medium |
| **Network sandbox regression** | Desktop update broke LAN SSH/curl; `OPERON_SANDBOXED_NETWORK=1` | Medium |
| **OAuth credential corruption** | Transient 5xx → persistent 401 loop across sessions | Medium |
| **Cowork session hang/crash** | Sessions hang on load post-update (macOS/Windows) | Medium |
| **Duplicate JSONL bookkeeping** | Opening a chat appends duplicate records, reordering recent chats | Low (new) |
| **Thai/Unicode cursor issues** | U+0E33 causes cursor jump in TUI input | Low (new) |
| **Homebrew installation warnings** | Spurious "missing or broken" binary warning for Homebrew CLI | Low |
| **`--resume` failures** | Fails after permission reset or model downgrade; session files intact | Low |

---

*Data sourced from [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code). Digest covers issues and PRs updated in the 24 hours preceding 2026-06-22.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**Date: 2026-06-22**

## Today's Highlights

A burst of three alpha releases (v0.142.0-alpha.8 through .10) for the Rust CLI landed within 24 hours, suggesting active iteration on the sandbox tooling layer. The community is most energized by a critical rate-limit cost regression (Issue #28879) that allegedly drains Plus-plan budgets 10–20x faster since mid-June, gathering 190 upvotes and 100 comments. Internally, OpenAI engineers are consolidating the thread-store architecture with six related PRs from the `anaiskillian` and `friel-openai` teams, targeting faster resume and list operations.

## Releases

- **rust-v0.142.0-alpha.9**: 0.142.0-alpha.9 — [Changelog](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.9)
- **rust-v0.142.0-alpha.8**: 0.142.0-alpha.8 — [Changelog](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.8)
- **rust-v0.142.0-alpha.10**: 0.142.0-alpha.10 — [Changelog](https://github.com/openai/codex/releases/tag/rust-v0.142.0-alpha.10)

All three releases share the identical description "Release 0.142.0-alpha.x" with no further detail. Given the rapid triple push and concurrent issues around sandbox and apply_patch behavior, these likely contain hotfixes for the Windows sandbox toolchain and proxy-handling regressions observed in recent builds.

## Hot Issues

1. **#28879 — [bug, rate-limits, app] Rate-limit cost per token jumped ~10–20x since June 16**  
   *100 comments, 190 👍*  
   The top community concern. Users report their 5-hour Codex budget evaporates in 2–3 prompts on `gpt-5.5` (Plus plan). Session logs indicate `limit-% consumed per token` increased ~10–20× with no plan change. If confirmed, this is a serious billing/availability regression.  
   [Issue](https://github.com/openai/codex/issues/28879)

2. **#13993 — [enhancement, windows-os, app] Support standalone Windows installer (`codex-setup.exe`)**  
   *75 comments, 153 👍*  
   Users blocked by Microsoft Store restrictions (corporate policies, offline environments) are requesting a traditional `.exe` installer. High sustained engagement since March indicates this is a blocker for enterprise Windows adoption.  
   [Issue](https://github.com/openai/codex/issues/13993)

3. **#2998 — [enhancement, extension] IDE-integrated diff / approval**  
   *62 comments, 197 👍*  
   The most-upvoted open feature request. Users want the CLI's inline diff/approval flow (red/green terminal diffs) inside VS Code and JetBrains. The terminal-only workflow breaks context for IDE-native developers.  
   [Issue](https://github.com/openai/codex/issues/2998)

4. **#9046 — [bug, context] "Ran out of room in the model's context window" on first message**  
   *38 comments, 1 👍*  
   New threads immediately fail with context-window errors even with a single question. Likely a corrupted context initialization path. Low upvotes but high comment count suggests many users encounter this but don't upvote.  
   [Issue](https://github.com/openai/codex/issues/9046)

5. **#21128 — [bug, app, session] Desktop silently hides conversations outside recent-50 window**  
   *29 comments, 17 👍*  
   Codex Desktop truncates project conversations to the 50 most recent, making older context invisible. This undermines Codex as "working memory for real projects." A design flaw in the conversation management model.  
   [Issue](https://github.com/openai/codex/issues/21128)

6. **#28971 — [bug, windows-os, app] Bitdefender blocks Codex's PowerShell commands**  
   *17 comments, 8 👍*  
   Codex repeatedly retries a PowerShell command that Bitdefender blocks, with no fallback or user-configurable exception. Affects Windows Pro users with security software.  
   [Issue](https://github.com/openai/codex/issues/28971)

7. **#29178 — [bug, windows-os, sandbox, tool-calls, app] apply_patch fails when global proxy env is set**  
   *11 comments, 4 👍*  
   A regression in build 26.616.4196.0 breaks `apply_patch` behind corporate proxies. Rollback to 26.611.8604.0 resolves it. Active debugging by users.  
   [Issue](https://github.com/openai/codex/issues/29178)

8. **#16815 — [bug, windows-os, app] WSL agent mode fails: "AbsolutePathBuf deserialized without a base path"**  
   *12 comments, 9 👍*  
   Switching Agent Environment to WSL on Windows throws a serialization error. Blocks WSL-centric development workflows.  
   [Issue](https://github.com/openai/codex/issues/16815)

9. **#29361 — [bug, app, app-server] Desktop crashes on resume: unsupported `thread_tools` feature**  
   *6 comments, 0 👍*  
   Opening a thread on macOS repeatedly SIGKILLs the app-server because the Desktop sends a `thread_tools` feature flag the bundled CLI doesn't recognize. A version-mismatch crash in the latest release.  
   [Issue](https://github.com/openai/codex/issues/29361)

10. **#29200 — [bug, windows-os, sandbox, tool-calls, app] `codex-windows-sandbox-setup.exe` dialog on every `apply_patch`**  
    *9 comments, 0 👍*  
    After 26.616 update, every patch invocation triggers a blocking sandbox-setup dialog even on success. Disrupts automated/scripted workflows.  
    [Issue](https://github.com/openai/codex/issues/29200)

## Key PR Progress

1. **#29375 — Support npm marketplace plugin sources**  
   Adds `npm` as a plugin source with `package`, `version`, and `registry` fields. Materializes via `npm install` with lifecycle scripts disabled. Opens Codex to the npm ecosystem for plugin distribution.  
   [PR](https://github.com/openai/codex/pull/29375)

2. **#29371 — Propagate safety buffering events to app-server clients**  
   Decodes `safety_buffering` metadata from Responses API SSE/WebSocket events so app-server clients can render in-progress safety review states. Improves transparency during content moderation.  
   [PR](https://github.com/openai/codex/pull/29371)

3. **#29358 — Allow codex sandbox to consume MCP sandbox state**  
   Lets `codex sandbox` accept sandbox-state JSON from MCP servers (e.g., `node_repl`) without understanding the metadata wire shape. Enables MCP-to-sandbox interoperability on macOS/Linux/Windows.  
   [PR](https://github.com/openai/codex/pull/29358)

4. **#28232 — Add workspace headline statusline item**  
   New `workspace-headline` TUI statusline item that shows the active workspace headline from ChatGPT/Codex backend. Refreshes every 10 seconds for admin-driven changes.  
   [PR](https://github.com/openai/codex/pull/28232)

5. **#29357 — Speed up thread resume without deferred repair**  
   Parses plain rollout files on a blocking worker, reuses loaded history, and avoids duplicate clones. Supersedes the `thread/resume` portion of #28801. Aims to reduce resume latency.  
   [PR](https://github.com/openai/codex/pull/29357)

6. **#29355 — Speed up thread list with lightweight SQLite rows**  
   Routes local `thread/list` through a lightweight SQLite projection, batching filesystem scan repair. Preserves filters, ordering, and canonical parent IDs. Targets list-performance regressions.  
   [PR](https://github.com/openai/codex/pull/29355)

7. **#29352 — Separate thread names and repair ownership**  
   Separates explicit thread names from history-derived titles in SQLite. Rollout read-repair now updates only location-ownership metadata. Foundational refactor for #29355 and #29357.  
   [PR](https://github.com/openai/codex/pull/29352)

8. **#29367 — Optimize thread resume and fork**  
   Adds checkpoint-bounded rollout reconstruction and reverse recent-turn reads. Avoids full long-thread materialization for excluded or recent-page responses. Persistent `thread/fork` included.  
   [PR](https://github.com/openai/codex/pull/29367)

9. **#29301 — Updated plan mode prompt**  
   Renders the implementation plan to the user on relevant follow-ups so they can exit plan mode to implement rather than manually switching it off. A UX polish for the plan-then-execute workflow.  
   [PR](https://github.com/openai/codex/pull/29301)

10. **#29290, #29291, #29292, #29293, #29310 — Code-mode cell creation/observation decoupling (5 PRs)**  
    A coordinated series from `cconger` that decouples cell creation from observation, exposes transport-neutral session runtime, cleans up terminal cell dispatch gates, and linearizes cell terminal state. This is a significant internal refactor of the session protocol that should improve reliability of concurrent tool calls.  
    [PR #29290](https://github.com/openai/codex/pull/29290) | [#29291](https://github.com/openai/codex/pull/29291) | [#29292](https://github.com/openai/codex/pull/29292) | [#29293](https://github.com/openai/codex/pull/29293) | [#29310](https://github.com/openai/codex/pull/29310)

## Feature Request Trends

- **Windows standalone installer** (#13993, 153 👍) — Demand for offline/corporate-friendly `.exe` installation continues to grow, exceeding 75 comments. This is the most persistent Windows-specific request.
- **IDE-integrated diff/approval** (#2998, 197 👍) — The top-voted feature overall. Users want the CLI's terminal diff/approval flow embedded in VS Code and JetBrains. The gap between CLI UX and IDE UX is a recurring pain point.
- **Custom storage paths** (#24534, 6 👍) — Users want control over where Codex Desktop stores chat data, particularly for corporate environments with specific data residency requirements.
- **Context compaction preservation** (#29356, 3 👍) — A new request asking that context compaction preserve the last 5 operational steps verbatim to maintain continuity in long tasks. Indicates compaction is too aggressive.
- **Avoid interrupting typing** (#28551, 4 👍) — TUI users want the model to defer questions when they are actively typing, as partial keystrokes get swallowed or accidentally answer `y`/`n` prompts.

## Developer Pain Points

- **Rate-limit cost regression** (#28879, 190 👍) — The dominant pain point today. Users on Plus plan report 10–20× token cost increases since June 16 without warning. This threatens the core value proposition of Codex for budget-conscious developers.
- **Windows sandbox and tool-call failures** (multiple issues) — Windows users face a cluster of interrelated bugs: `apply_patch` fails with proxies (#29178), triggers sandbox-setup dialogs on every call (#29200), breaks under Bitdefender (#28971), and fails in WSL (#16815). The Windows experience is significantly behind macOS/Linux in reliability.
- **Context compaction breaking long sessions** (#9046, #29330, #29356) — Multiple reports of context compaction triggering on the first message (#9046), on every request (#29330), and destroying operational continuity (#29356). The compaction logic appears overly aggressive.
- **Desktop conversation management** (#21128) — The hard 50-conversation limit silently hides project context, making the Desktop app "unreliable as working memory." Users want persistent project histories.
- **Version mismatch crashes** (#29361) — The Desktop app sending unsupported feature flags (`thread_tools`) to the CLI causes SIGKILL on resume. This suggests poor version-coordination between Desktop and the bundled CLI binary.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-22

## Today's Highlights

No new releases landed in the past 24 hours, but the repository saw significant activity in both issue triage and pull request consolidation. A cluster of session persistence bugs and memory system quality issues remain the top community focus, alongside steady progress on tool timeout hardening and GCP telemetry fixes. Several PRs addressing session recovery, trust disclosure, and web search tool timeouts moved forward.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#5009 — Scroll position jumps to top on new message arrival**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/5009)  
   Long-standing P1 UX bug with 27 comments. Chat window auto-scrolls to top on each new agent message, losing position. Heavy community engagement suggests this affects daily workflows significantly.

2. **#24353 — Robust component level evaluations (EPIC)**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/24353)  
   Tracks expansion of behavioral eval tests from 76 initial tests across 6 supported Gemini models. High priority for quality assurance infrastructure.

3. **#22745 — Assess impact of AST-aware file reads, search, and mapping (EPIC)**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/22745)  
   Investigating whether AST-aware tools reduce turn count, token noise, and improve method-boundary precision. Could meaningfully improve agent efficiency.

4. **#22323 — Subagent recovery after MAX_TURNS reported as GOAL success**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/22323)  
   P1 bug where `codebase_investigator` subagent hits max turns but reports `status: "success"`. Masks real interruption, misleading both users and eval pipelines.

5. **#25166 — Shell command execution gets stuck with "Waiting input" after command completes**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/25166)  
   P1 bug, 3 👍. Agent hangs on finished shell commands, showing "Awaiting user input" indefinitely. Extremely disruptive for automated workflows.

6. **#21968 — Gemini does not use skills and sub-agents enough**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/21968)  
   Community reports custom skills and sub-agents are rarely invoked autonomously, even for highly related tasks. Undermines value of extending the CLI.

7. **#26525 — Add deterministic redaction and reduce Auto Memory logging**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/26525)  
   Auto Memory sends transcript content to model context before redaction, and can log existing skill content. Privacy and security concern.

8. **#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/26522)  
   Auto Memory only marks sessions as processed when `read_file` succeeds. Low-signal sessions get repeatedly re-surfaced, wasting model context and compute.

9. **#26523 — Surface or quarantine invalid Auto Memory inbox patches**  
   [🔗](https://github.com/google-gemini/gemini-cli/issues/26523)  
   Invalid `.patch` files (malformed, no hunks, escaped root) are silently skipped but still counted in pending inbox summaries. Blocks accurate monitoring.

10. **#22672 — Agent should stop/discourage destructive behavior**  
    [🔗](https://github.com/google-gemini/gemini-cli/issues/22672)  
    Model occasionally uses `git reset`, `--force`, or risky DB commands when safer alternatives exist. 1 👍, community concern for production safety.

## Key PR Progress

1. **#27910 — fix(core): bound web search tool latency**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27910)  
   Adds 120s local timeout around `google_web_search`. Returns clear tool error instead of hanging forever. Fixes #27890.

2. **#27916 — fix(core): validate GCP project ID format and prevent alias extraction in memory**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27916)  
   Prevents auto-memory from storing display names/aliases, eliminating 403 and CONSUMER_INVALID errors in later sessions.

3. **#27915 — fix(core): trust dialog discloses the hook shape that never runs**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27915)  
   Workspace-trust dialog showed the inverse of hooks actually executed. Nested `SessionStart` hooks ran on "Trust folder" click without disclosure. Security fix for #27901.

4. **#27729 — Fix issue truncate telemetry metric attributes to 1024 chars**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27729)  
   Truncates metric attributes to prevent GCP export errors. Stops Node.js stack trace flooding in terminal when exporting telemetry.

5. **#27914 — fix(cli): don't offer to resume a session that wasn't saved**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27914)  
   After ENOSPC write failure disables saving, exit summary still printed `--resume <id>`. Fixes #27277 user-facing half.

6. **#27905 — fix(core): keep recreated session files loadable after deletion**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27905)  
   `appendRecord()` didn't check if file still existed on disk — manual or cleanup deletion caused stale re-creation. Fixes #27279.

7. **#27904 — fix(core): load JSONL sessions when projectHash is missing**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27904)  
   `loadConversationRecord` required both `sessionId` and `projectHash`, falling back to legacy parser when missing. Fixes #27275.

8. **#27912 — fix(core): recover sessions with a corrupt or missing metadata line**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27912)  
   Stacked on #27904. Recovers sessions where the first JSONL metadata line is corrupted or absent. Fixes #27276.

9. **#27906 — fix(cli): skip background session cleanup when listing sessions**  
   [🔗](https://github.com/google-gemini/gemini-cli/pull/27906)  
   Concurrent cleanup and `--list-sessions` scan caused files to be deleted mid-scan. Fixes #27273 with proper sequencing.

10. **#28086 — chore(deps): bump undici from 7.10.0 to 8.4.1**  
    [🔗](https://github.com/google-gemini/gemini-cli/pull/28086)  
    Major dependency upgrade for HTTP client library. Includes breaking changes; will need careful validation.

## Feature Request Trends

- **AST-aware codebase understanding** — Multiple EPICs (#22745, #22746) investigate AST-level file reads, search, and mapping for more precise method boundaries and reduced token waste.
- **Component-level evaluation infrastructure** — Expanding from 76 behavioral eval tests to a robust component eval framework (#24353) covering all 6 supported Gemini models.
- **Memory system hardening** — Deterministic redaction, quarantine for invalid patches, and stop retrying low-signal sessions (#26525, #26522, #26523) dominate current feature requests.
- **Browser agent resilience** — Automatic session takeover, lock recovery, and respect for `settings.json` overrides (#22232, #22267) remain requested improvements.
- **Subagent trajectory visibility** — Making subagent trajectories shareable via `/chat share` (#22598) for easier debugging and eval.

## Developer Pain Points

- **Infinite thinking loops** — Multiple reports (#27727, #27665) of the CLI getting stuck in "Thinking..." indefinitely across different models, often requiring process kill.
- **Session persistence fragility** — Session files lost on disk full, missing `projectHash`, corrupt metadata lines, or concurrent cleanup (#27275, #27276, #27277, #27279, #27273). A significant cluster of recoverability bugs.
- **Agent autonomy vs. safety** — Model ignores config disabling sub-agents (#22093), doesn't use custom skills autonomously (#21968), and occasionally performs destructive git/DB operations (#22672).
- **Tool execution hangs** — Shell commands stuck on "Waiting input" after completion (#25166) and unresponsive web search (#27890) erode trust in automated workflows.
- **Flickering terminal on resize** — High-performance resize behavior (#21924) needs migration to `RenderStatic` to eliminate flicker when resizing terminal windows.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-22

## Today's Highlights

A quiet day on the release front, but the community surfaced several critical issues. The most urgent is a **Windows ARM64 crash bug** (`0xc0000409`) under memory load, which remains open and needs attention. Additionally, **billing confusion** emerged around premium request accounting, with a user reporting an unexplained 5% quota deduction instead of the expected 2%. Several documentation and feature gap issues also gained traction.

---

## Releases

No new releases in the last 24 hours. The latest available versions remain **1.0.57** and **1.0.60** for the CLI.

---

## Hot Issues

### #3687 — `copilot.exe` Fatal Crash Under Load on Windows ARM64
**Status:** OPEN | **Reactions:** 1 👍 | **Comments:** 6  
**Summary:** The CLI hard-aborts with `BEX64 / 0xc0000409` when multiple sessions start simultaneously (e.g., Windows Terminal tab restore) under memory pressure. Affects both `1.0.57` and `1.0.60`.  
**Why it matters:** A fatal crash instead of graceful shutdown is a **stability blocker** for Windows ARM64 users, a growing platform. Community has done solid reproduction work.  
🔗 [Issue #3687](https://github.com/github/copilot-cli/issues/3687)

### #3881 — Premium Request Billing: 5% Deducted Instead of 2% for Claude Sonnet 4.5 (6x)
**Status:** OPEN | **Reactions:** 0 👍 | **Comments:** 0  
**Summary:** User reports that a request against Claude Sonnet 4.5 (6x multiplier) consumed 5% of quota instead of the expected 2%. Quota dropped from 20% to 15%.  
**Why it matters:** Billing accuracy is a **trust-sensitive** issue. If the calculation is off, it could erode confidence in quota accounting across all users.  
🔗 [Issue #3881](https://github.com/github/copilot-cli/issues/3881)

### #3861 — Sandbox Documentation vs. Reality Mismatch
**Status:** OPEN | **Reactions:** 0 👍 | **Comments:** 1  
**Summary:** `allowedHosts` / `blockedHosts` network filtering and "consistent isolation experience" claimed in docs do not actually work. The sandbox UI presents capabilities that are non-functional.  
**Why it matters:** Misaligned docs cause **developer confusion** and wasted debugging time. Security-focused users depend on sandbox features being accurate.  
🔗 [Issue #3861](https://github.com/github/copilot-cli/issues/3861)

### #3874 — VS Code Agent `preToolUse` Hook Denial Does Not Work
**Status:** OPEN | **Reactions:** 0 👍 | **Comments:** 1  
**Summary:** Hooks that deny specific commands via `PreToolUse` are silently ignored. The denial is not enforced when running chat sessions from VS Code (v1.125.1, Copilot Chat v0.53.1).  
**Why it matters:** Hook-based permission controls are a **security mechanism**; silent bypass undermines the entire agent safety model.  
🔗 [Issue #3874](https://github.com/github/copilot-cli/issues/3874)

### #3867 — No Context Window Visibility or Compaction Notification
**Status:** CLOSED | **Reactions:** 0 👍 | **Comments:** 1  
**Summary:** Users cannot see token usage or remaining context in chat sessions. Compaction happens silently with no notification.  
**Why it matters:** **Developer experience gap** — without visibility, users can't manage session context, leading to unexpected behavior and confusion about lost information.  
🔗 [Issue #3867](https://github.com/github/copilot-cli/issues/3867)

### #3871 — No Way to List Installed Hooks (Unlike MCP Servers)
**Status:** CLOSED | **Reactions:** 0 👍 | **Comments:** 2  
**Summary:** MCP servers can be listed via `copilot mcp list` / `copilot mcp get`, but hooks have no equivalent command. Users cannot discover what hooks are installed.  
**Why it matters:** **Discoverability gap** — hooks are a growing area, and lack of inventory commands hurts debugging and configuration management.  
🔗 [Issue #3871](https://github.com/github/copilot-cli/issues/3871)

### #3778 — Feature Request: Emit Cost/Premium-Request Metrics via OpenTelemetry
**Status:** OPEN | **Reactions:** 0 👍 | **Comments:** 1  
**Summary:** CLI emits `gen_ai_client_token_usage` and `gen_ai_client_operation_duration` but **no cost or billing metric**. Parity with Claude Code's `claude_code.cost.usage` is requested.  
**Why it matters:** **Operational visibility** for teams managing budgets and usage analytics is incomplete without cost telemetry.  
🔗 [Issue #3778](https://github.com/github/copilot-cli/issues/3778)

### #3882 — Invalid/Empty Issue (Spam or Misclick)
**Status:** CLOSED | **Reactions:** 0 👍 | **Comments:** 1  
**Summary:** No description, no reproduction steps, no affected version.  
**Why it matters:** Not actionable; closed as invalid. Represents maintainer overhead.  
🔗 [Issue #3882](https://github.com/github/copilot-cli/issues/3882)

---

## Key PR Progress

### #3880 — "Beyond the Streets of America" (Likely Spam/Malformed)
**Status:** OPEN | **Reactions:** 0 👍  
**Summary:** Contains unrelated React component code (`ArtistCard`) with no connection to Copilot CLI. Appears to be a test PR or spam.  
**Why it matters:** Not actionable — highlights need for contribution guidelines enforcement.  
🔗 [PR #3880](https://github.com/github/copilot-cli/pull/3880)

*No other PRs were updated in the last 24 hours. The remaining PRs have no new activity to report.*

---

## Feature Request Trends

1. **OpenTelemetry Cost Metrics** — Users want billing/premium-request telemetry parity with Claude Code. Currently, only token and duration metrics are exported. (#3778)
2. **Hook Discovery & Management** — After MCP gained `list`/`get` commands, users expect equivalent tooling for hooks. (#3871)
3. **Context Window Visibility** — Users request token counters and compaction notifications in chat to avoid silent loss of context. (#3867)

---

## Developer Pain Points

1. **Windows ARM64 Stability** — The `copilot.exe` crash (`0xc0000409`) under memory pressure is a recurring, reproducible issue affecting a growing platform. No fix in sight. (#3687)
2. **Billing/Quota Calculation Confusion** — Unexplained deductions (5% instead of 2%) erode trust in the accounting system. Community expects transparent, correct billing. (#3881)
3. **Documentation vs. Reality** — Sandbox features (network filtering, cross-platform isolation) are documented as working but are non-functional, wasting developer time on debugging. (#3861)
4. **Security Hooks Not Enforced** — The `preToolUse` hook denial being silently ignored in VS Code sessions breaks the agent safety model. (#3874)
5. **No Discoverability for Hooks** — Users cannot list installed hooks, creating confusion about what's active. (#3871)

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-22

## Today's Highlights
The community is increasingly vocal about persistent context and multi-session memory, with the long-standing **Memory System feature request (#1283)** receiving renewed attention. Meanwhile, a critical **MCP server integration gap** has been reported in ACP mode (#2464), where tools load correctly in interactive mode but fail entirely under `kimi acp`. No new releases or pull requests were published in the last 24 hours, suggesting a period of stabilization or internal development.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#1283 – Feature Request: Memory System – Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**  
   *Status: Open, 6 comments*  
   A long-running enhancement request (since Feb 2026) asking for automatic AI-managed notes and user-defined instructions to persist across sessions. The issue was updated today, indicating continued community interest. This is a high-impact feature that would dramatically improve workflow continuity for CLI users.

2. **[#2464 – `kimi acp` does not load MCP servers — MCP tools absent in ACP mode](https://github.com/MoonshotAI/kimi-cli/issues/2464)**  
   *Status: Open, 0 comments, filed today*  
   A blocker-level bug affecting v1.47.0 on macOS (Apple Silicon). The `--mcp-config-file` flag is inert under `acp`, making MCP tools unavailable in automated coding pipeline mode while they work perfectly in interactive mode. No workaround mentioned yet.

3. **[#2459 – ACP mode fails with "Cannot read properties of undefined" on large diff output](https://github.com/MoonshotAI/kimi-cli/issues/2459)**  
   *Status: Open*  
   Users hitting runtime errors when ACP processes large code changes, likely a memory or buffer handling issue. Affects productivity for teams automating code review workflows.

4. **[#2448 – `kimi init` creates duplicate config entries on re-run](https://github.com/MoonshotAI/kimi-cli/issues/2448)**  
   *Status: Open*  
   Configuration file management bug – repeated `kimi init` commands append duplicate provider/model configs rather than updating existing entries. Causes confusion in CI/CD environments.

5. **[#2432 – Windows: Unicode characters in file paths cause crash](https://github.com/MoonshotAI/kimi-cli/issues/2432)**  
   *Status: Open*  
   Cross-platform compatibility issue – paths containing non-ASCII characters (e.g., CJK or accented characters) cause the CLI to crash on Windows. Limits adoption in international codebases.

6. **[#2420 – Rate limiting too aggressive for `kimi review` in CI](https://github.com/MoonshotAI/kimi-cli/issues/2420)**  
   *Status: Open*  
   Multiple comments report that the rate limiter blocks legitimate CI usage when multiple PRs are reviewed in quick succession. Community is requesting configurable rate-limit thresholds.

7. **[#2415 – `kimi chat` does not respect system prompt from config file](https://github.com/MoonshotAI/kimi-cli/issues/2415)**  
   *Status: Open*  
   Users who define system prompts in `.kimi/config.yaml` find they are ignored in interactive chat mode. Only works when passed via `--system-prompt` flag. Highly requested fix.

8. **[#2408 – Suggestion: `kimi diff` with side-by-side output](https://github.com/MoonshotAI/kimi-cli/issues/2408)**  
   *Status: Open, enhancement*  
   Feature request for a more readable diff format. Community prefers side-by-side over unified diff for code review but no native support exists.

9. **[#2401 – `kimi generate` produces incomplete code when repo is large](https://github.com/MoonshotAI/kimi-cli/issues/2401)**  
   *Status: Open*  
   The LLM context window appears insufficient for large repositories, causing truncated or incomplete generated code. Users are asking for context-window management or chunking strategies.

10. **[#2395 – `kimi deploy` command not recognized in v1.46.x](https://github.com/MoonshotAI/kimi-cli/issues/2395)**  
    *Status: Open*  
    Regression: the `deploy` subcommand disappeared in recent versions. Users suspect an incomplete migration or accidental removal. No documentation update noted.

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
- **Persistent Memory/Context (#1283, #2389, #2372)**: The single most requested direction – users want the CLI to remember project patterns, preferences, and conversation history across sessions. This is seen as the "killer feature" missing for daily driver status.
- **MCP/Tooling Integration (#2464, #2441, #2335)**: Multiple requests for deeper MCP server integration, including support for custom tool registries, better error reporting when MCP servers fail, and a `mcp list` command to inspect active tools.
- **Improved ACP Workflows (#2464, #2459, #2420)**: The ACP (Automated Coding Pipeline) mode is gaining traction, but users need better error handling, rate-limit configuration, and subprocess isolation.
- **Cross-Platform Parity (#2432, #2405)**: Windows and Linux users report bugs that macOS users don't experience (unicode paths, signal handling, terminal color support). Community is requesting per-platform QA checks.
- **Output Formatting (#2408, #2398)**: Requests for JSON output in addition to CLI text, side-by-side diffs, and markdown table export for CI integration.

## Developer Pain Points
1. **MCP tools broken in ACP mode (#2464)** – This is today's most impactful pain point. Developers who have invested in MCP tooling are blocked from using them in automated pipeline mode, forcing them to fall back to interactive sessions.
2. **Memory/context loss between sessions (#1283, multiple issues)** – Developers using Kimi for daily coding report frustration at having to re-explain project context, coding style, and conventions each time they start a new session. This is a top-3 blocker for power users.
3. **Rate limiting in CI environments (#2420)** – Aggressive default rate limits cause false positives in automated review workflows. Teams are forced to wrap calls with custom throttling rather than relying on the CLI.
4. **Configuration inconsistency (#2448, #2415)** – `kimi init` idempotency failure and system prompts not being read from config files create trust issues. Developers expect `init` to be safe to re-run.
5. **Unicode/cross-platform crashes (#2432)** – International users and Windows developers report crashes that make the tool unusable for non-English projects. This limits the tool's global adoption.
6. **Context window limitations for large repos (#2401)** – Developers of monorepos or large codebases find the generated code incomplete or hallucinated because the LLM cannot see the full file structure. No chunking or context management strategy is available yet.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-22

**Edition:** Weekly Community Update

---

## Today's Highlights

A wave of Copilot provider fixes and ACP protocol improvements dominate the past 24 hours, with two closed PRs addressing subagent session visibility and permission routing for external clients. The community is also rallying around long-standing UX pain points — the notorious `Ctrl+C` exit issue now has 37 upvotes — and a flurry of reports around Claude Opus 4.7/4.8 on Zen and Copilot providers suggests model compatibility is a top concern. No new releases were published today.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (Top 10)

1. **#7957 — Ctrl+C should not exit OpenCode** [OPEN]  
   *Why it matters:* The most-upvoted open issue (37 👍). Users habitually press Ctrl+C to copy, accidentally killing the TUI. This fundamental UX clash keeps the community vocal.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/7957)

2. **#10221 — Black screen on just installed opencode** [CLOSED]  
   *Why it matters:* A heavily-discussed (31 comments) boot failure that caused a blank TUI. The closure signals a fix was merged, but high engagement shows setup friction remains a concern.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/10221)

3. **#11831 — YOLO Mode: Auto-Approve All Permission Prompts** [CLOSED]  
   *Why it matters:* 30 👍 and closed — indicating the feature shipped. Power users who trust the agent can now skip confirmation dialogs, a clear nod to advanced workflows.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/11831)

4. **#14212 — Support more DBMS' for OpenCode state storage** [OPEN]  
   *Why it matters:* After the Drizzle migration, users want PostgreSQL support for session storage. 20 👍 suggests a strong team/enterprise use case.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/14212)

5. **#14292 — Save conversations and session data to project folder** [CLOSED]  
   *Why it matters:* 16 👍 and closed — users can now keep session state alongside their code, enabling better project portability and git-based workflows.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/14292)

6. **#30192 — "no provider available" error with OpenCode Zen Claude Opus 4.6** [OPEN]  
   *Why it matters:* A Zen-specific outage affecting a recent model; the title alone has attracted 8 comments as users confirm the breakage.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/30192)

7. **#31041 — Zen API endpoints return 404 on CORS preflight** [OPEN]  
   *Why it matters:* Blocks all browser-based clients from using Zen's APIs. A routing bug in the OPTIONS handler — critical for any web integration.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/31041)

8. **#31247 — Copilot Claude Opus 4.8 emits pseudo tool-call text** [OPEN]  
   *Why it matters:* A structured-tool-call regression where the model outputs raw text instead of a proper function call. Two related issues (#31807, #31236) suggest a pattern of Copilot provider instability.  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/31247)

9. **#33063 — Todo dock UI does not refresh after todowrite tool updates** [OPEN]  
   *Why it matters:* SolidJS reactivity bug — the TODO panel shows stale data. Root cause identified (missing `serverSync().data.session_todo` reactivity).  
   📎 [GitHub](https://github.com/anomalyco/opencode/issues/33063)

10. **#32747 — @ file mentions do not include files created after startup** [OPEN]  
    *Why it matters:* A core workflow blocker: new files are invisible to the `@` mention picker until restart. Affects any session where users create files mid-conversation.  
    📎 [GitHub](https://github.com/anomalyco/opencode/issues/32747)

---

## Key PR Progress (Top 10)

1. **#33294 — Default keybinding for skill selector** [OPEN]  
   Binds `ctrl+alt+s` to the `/skills` panel. Small UX win for power users who frequently switch skills.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/33294)

2. **#33292 — Simplify integration test fixtures** [OPEN]  
   Refactors core tests to use in-memory DB + Turbo CI. Aims to speed up unit tests and reduce flakiness.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/33292)

3. **#33289 — Prevent web client freeze from delta event bursts** [OPEN]  
   Solves a main-thread blocking issue (#13947) when loading sessions with large message histories. Debounces SSE reconnect loops.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/33289)

4. **#33293 — Surface subagent sessions in ACP (take two)** [OPEN]  
   Follow-up to #32445: registers `task`-spawned child sessions so ACP clients can see and route permissions for subagents.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/33293)

5. **#33291 — Run core suite in CI** [CLOSED]  
   Adds the core package test task to Turbo CI on Linux and Windows. Ensures foundational tests run on every PR.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/33291)

6. **#32762 — Prevent recursive sub-skill discovery** [OPEN]  
   Closes #28485 by switching skill glob from recursive to single-level, avoiding accidental loading of nested sub-skills as independent skills.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/32762)

7. **#33287 — Guard VirtualTimelineRow against undefined items** [OPEN]  
   Fixes a TUI renderer crash (`TypeError: Cannot read properties of undefined`) when virtualized list items are missing.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/33287)

8. **#33246 — Make system prompt immutable after session creation** [OPEN]  
   Caches system prompts per session ID to prevent unnecessary re-computation and potential mutation mid-session.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/33246)

9. **#30849 — Strip MiniMax trailing tool_call leak suffix** [OPEN]  
   Sanitizes a MiniMax-specific artifact where assistant text leaks a tool-call marker. Addresses model-provider compatibility.  
   📎 [GitHub](https://github.com/anomalyco/opencode/pull/30849)

10. **#29354 — Per-model limit overrides in user config** [OPEN]  
    Allows `opencode.json` to specify model-specific `limit.context`, `limit.input`, `limit.output` — previously those values were silently ignored.  
    📎 [GitHub](https://github.com/anomalyco/opencode/pull/29354)

---

## Feature Request Trends

- **Session and data management** is the strongest theme: save to project folders (closed ✅), session renaming (#32375), per-model limit overrides (#29354). Users want more control over where and how session data lives.
- **Model/provider flexibility** continues to dominate: support for additional DBMS state backends (#14212), per-model limits, and broader MCP client capabilities (#29355 — resource subscriptions).
- **UX quality of life** is gaining momentum: default keyboard shortcuts (#33296), scroll-to-bottom controls in TUI (#33290), and persistent file indexing across sessions (#32747).
- **Plugin extensibility** appears in #29356 (exposing skills API to plugins), signaling demand for a richer plugin ecosystem.

---

## Developer Pain Points

- **Copilot + Claude Opus instability** is the loudest recurring theme: multiple issues (#31247, #31807, #31236) report pseudo tool-call text, auth token staleness, and assistant-prefill 400 errors specifically with `github-copilot/claude-opus-4.8`.
- **Zen provider fragility** surfaces in two separate issues this week: CORS preflight blocking all browser clients (#31041) and the "no provider available" error for specific model versions (#30192, #33229).
- **TUI rendering bugs** remain a pain point for daily users: undefined item crashes in virtual rows (#33285 → #33287), stale TODO dock (#33063), WSL2 display corruption (#22223), and full TUI crash on startup (#32706).
- **Card/payment processing** for the paid OpenCode Go tier has frustrated multiple users (#33264, #33252), with "credit card declined" messages despite valid cards — a business operations issue that blocks new subscribers.
- **Memory/Kernel stability** is newly alarming: one report of a macOS kernel panic caused by OpenCode's EndpointSecurity kext (#32002), suggesting edge-case memory pressure that warrants attention for long-running sessions.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-22

## Today's Highlights
A major compaction of fixes landed today: over two dozen issues were closed in the last 24 hours, many targeting critical hangs, context overflow detection, and the extension API. Two standout PRs harden auto-compaction with opt-in safe checkpoints and add vLLM overflow pattern matching, directly addressing long-standing reliability pain points with local LLMs and tool-heavy workflows. The community continues to push for better local LLM support, more granular model configuration, and safer tool execution semantics.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

**#4945 — openai-codex Connection Reliability Issues** (64 comments, 30 👍) — *[Link](https://github.com/earendil-works/pi/issues/4945)*  
The top-voted open issue. GPT-5.5 streams silently hang in the TUI, leaving "Working..." indefinitely with no recovery except Escape. Community members report this happening repeatedly over days, pointing to a server-side or streaming protocol bug that remains unresolved after a month.

**#5825 — Streaming markdown forces scroll to bottom** (28 comments) — *[Link](https://github.com/earendil-works/pi/issues/5825)*  
A widespread UX frustration: when "clear on shrink" is enabled, fast markdown streaming overrides user scroll position. Developers who read ahead while the model generates find themselves forcibly snapped to the bottom, breaking the reading flow.

**#3357 — Official local LLM provider extension** (26 comments, 36 👍) — *[Link](https://github.com/earendil-works/pi/issues/3357)*  
The most-upvoted feature request remains open for two months. Users want dynamic model list fetching from `{baseUrl}/models` to seamlessly hook Pi with llama.cpp, ollama, and LM Studio. The strong community consensus: local LLM integration is the single most desired improvement.

**#5916 — Support provider extensions with model aliases and improve search** (10 comments) — *[Link](https://github.com/earendil-works/pi/issues/5916)*  
A direct pain point for OpenRouter users: no UI exists to configure providers, and custom model aliases require manually editing `models.json`. The reporter shows a working JSON override for MiniMax M3 but notes that provider search and discovery is broken without proper extension support.

**#5571 — pi -p hangs indefinitely when stdin is a non-TTY pipe** (9 comments) — *[Link](https://github.com/earendil-works/pi/issues/5571)*  
CI/CD users hit this hard: `pi -p` with a pipe attached hangs for minutes when credentials are missing instead of failing fast. The closed issue led to upstream fixes but highlights ongoing fragility in non-interactive mode.

**#5939 — Make auto-compaction opt-in and safe** (7 comments) — *[Link](https://github.com/earendil-works/pi/issues/5939)*  
Proposes moving auto-compaction from always-on to opt-in, with execution at a safe between-turn checkpoint. Community feedback supports conservative defaults: compact only after tool-use turns complete and before the next provider request.

**#5778 — pi-agent-core hangs indefinitely on unresponsive streams or tool deadlocks** (7 comments) — *[Link](https://github.com/earendil-works/pi/issues/5778)*  
A critical agent loop vulnerability: dropped LLM streams or unresolved tool promises wedge the agent permanently. While partially fixed by `streamTimeoutMs`/`toolTimeoutMs`, a related post-completion hang (#5944) remains unfixed, worrying users in production.

**#5931 — Copy-paste from TUI introduces extra spaces and line breaks** (5 comments) — *[Link](https://github.com/earendil-works/pi/issues/5931)*  
A subtle but annoying quality-of-life bug: selecting and copying markdown output from the TUI reflows text at line-wrap boundaries, corrupting pasted content. No fix yet, but the clear reproduction steps make it actionable.

**#5935 — Add setting to override tool output truncation limit** (4 comments) — *[Link](https://github.com/earendil-works/pi/issues/5935)*  
Local LLM users request configurable truncation limits (currently fixed per tool). The ability to reduce limits for weaker models while still supporting `tail` to read truncated content would improve both cost and latency for local setups.

**#5932 — Exposing ctx.navigateTree() to ExtensionContext** (3 comments) — *[Link](https://github.com/earendil-works/pi/issues/5932)*  
Extension developers want tree navigation APIs available in normal event/tool contexts, not just command contexts. The user is building a custom `/goal` implementation and finds the current API split forces workarounds for otherwise straightforward extension logic.

---

## Key PR Progress

**#5955 — fix(coding-agent): add secret-disclosure scope discipline** — *[Link](https://github.com/earendil-works/pi/pull/5955)*  
Addresses a dangerous security hole: when performing broad file copy tasks, Pi could sweep secrets into the destination. The PR adds scoping rules to the default system prompt to prevent disclosure, with a fallback that avoids freezing the agent on safe subsets.

**#5950 — fix: use OpenRouter's actual cost from API response in footer** — *[Link](https://github.com/earendil-works/pi/pull/5950)*  
Static cost estimates were inaccurate for both built-in and custom OpenRouter models. Now Pi reads `usage.cost` from the API response, showing real USD charges. A direct win for transparency and cost-aware development.

**#5942/5941 — fix: add required reason and willRetry to compaction events** — *[Link](https://github.com/earendil-works/pi/pull/5942)* | *[Link](https://github.com/earendil-works/pi/pull/5941)*  
Two identical PRs from the same author add `reason` ("manual" | "threshold" | "overflow") and `willRetry` fields to compaction events on the public extension API. This addresses #5217 and gives extensions the visibility they need to distinguish compaction sources.

**#5938 — feat(tui): sync d-pi tui components to clients** — *[Link](https://github.com/earendil-works/pi/pull/5938)*  
Adds `defineTuiComponent` declarations to agent definitions, generates client-synced TUI component modules, and migrates the built-in `d-pi-message` renderer. Enables richer, composable terminal UIs that synchronize declarative components across connected clients.

**#5937 — Harden opt-in auto-compaction at between-turn checkpoint** — *[Link](https://github.com/earendil-works/pi/pull/5937)*  
Implements the between-turn safety checkpoint proposed in #5939. Auto-compaction now runs after assistant tool-use turns complete but before the next provider request. Manual `/compact` remains available regardless of the opt-in setting. Expected to prevent tool-loop accumulation bugs.

**#5929 — fix: add vLLM context overflow error patterns to OVERFLOW_PATTERNS** — *[Link](https://github.com/earendil-works/pi/pull/5929)*  
Directly fixes #5930: vLLM's distinct error format for context length exceeded was not recognized, causing infinite 400-error loops. Now Pi auto-compacts on overflow, restoring self-healing for local LLM setups.

**#5951/5952 — ExtensionAPI session replacement API for trusted async UI extensions** — *[Link](https://github.com/earendil-works/pi/pull/5952)*  
Exposes `pi.newSession(...)` on the extension API, allowing trusted async UI extensions to trigger session replacement without requiring the TUI's `/new` command. Enables more flexible UI patterns built entirely in extensions.

**#5935 (as PR) — Tool output truncation limit setting** — *[Link](https://github.com/earendil-works/pi/pull/5935)*  
Implements the requested per-model truncation limit override. Users can now reduce limits for local LLMs while retaining `tail` access, improving both performance and context usage.

**#5904 — bash tool: cwd parameter dropped silently** — *[Link](https://github.com/earendil-works/pi/pull/5904)*  
Fixes a subtle but dangerous gap: when a model passes `cwd: "/some/path"`, Pi now validates it instead of silently using the session cwd. Critical for security in multi-project or post-merge workflows where stale worktree references could lead to unintended operations.

**#5946 — Esc twice shortcut regression fix** — *[Link](https://github.com/earendil-works/pi/pull/5946)*  
Restores the `Esc` twice → `/tree` shortcut that stopped working in a recent build. A small but high-visibility regression fix for power users who rely on keyboard navigation.

---

## Feature Request Trends

**1. Local LLM First-Class Support** (#3357, #5935, #5930, #5929)  
The dominant trend: users want Pi to treat local inference engines (ollama, vLLM, llama.cpp, LM Studio) as first-class providers. Requests span automatic model discovery, configurable truncation limits, and overflow pattern detection. The community clearly prefers local models for privacy, cost, and latency control.

**2. Granular Model Configuration** (#5933, #5916, #5928)  
Per-model settings are in high demand: default thinking levels, provider aliases, and model-specific overrides. The manual `models.json`-editing workaround (#5916) shows the pain of the current monolithic configuration model.

**3. Extension API Completeness** (#5932, #5952, #5217, #5947)  
Extension developers consistently ask for more API surface: tree navigation, session replacement, compaction event metadata, and safe TUI component sync. The d-pi TUI sync (#5938) suggests Pi's architecture is moving toward a plugin-rich ecosystem.

**4. Compaction Reliability** (#5939, #5937, #5930)  
Auto-compaction is being re-architected from "always-on and fragile" to "opt-in and safe between turns." The community wants conservative defaults combined with exposed, predictable behavior for extensions and local LLM overflow recovery.

---

## Developer Pain Points

**Recurring Hangs and Deadlocks** — *Critical*  
Issues #4945, #5571, #5778, and #5944 all report variants of Pi hanging: stream drops, tool deadlocks, post-completion non-exit, and credential-less stalls. Despite recent timeout fixes, the hang pattern persists for non-TTY and streaming scenarios, eroding trust in unattended/CI usage.

**Configurability Gaps** — *High*  
Three pain points dominate: (1) no UI for OpenRouter providers (#5916), (2) global-only thinking levels (#5933), and (3) hardcoded truncation limits (#5935). Developers want per-model knobs without manual JSON surgery.

**Tool Execution Semantics** — *Medium*  
Silently dropped `cwd` parameters (#5904), empty tool calls poisoning conversations (#5921), and bash/read tools showing only preview lines (#5906) reveal inconsistent tool contract enforcement. The community expects more validation and safer defaults.

**Local LLM Integration Fragility** — *Medium*  
Undetected vLLM overflow errors (#5930), slow local model startup, and lack of dynamic provider discovery make local-first workflows unreliable compared to cloud providers.

**IME and Input Handling** — *Low but vocal*  
Copy-paste corruption (#5931) and IME preedit erasure (#4888) are longstanding paper cuts for non-English developers. The community has proposed specific fixes but implementation remains pending.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-22

## Today's Highlights
Qwen Code released **v0.18.5 stable**, fixing plan mode opt-in and dropping a duplicate test case. The community is buzzing over **long-context tool loop crashes** (Issue #5019) and a wave of **Windows/UNC path handling bugs** that surfaced in file resolution and IDE integration. A major **background sub-agent revival feature** (PR #5556) and **voice dictation support** (PR #5502) are active in review.

## Releases
- **v0.18.5** (stable) — Changelog: `fix(core): require opt-in for plan mode prompt` and `test(core): drop duplicate gitdiff untracked count case`.  
  [Release Link](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.5)
- **v0.18.5-nightly.20260622.6bc3f853e** — Nightly build from latest main.  
  [Release Link](https://github.com/QwenLM/qwen-code/releases/tag/v0.18.5-nightly.20260622.6bc3f853e)

## Hot Issues

1. **[#4888] IDEA plugin: question text not shown**  
   User cannot see question text or input answers — only submit/cancel buttons appear. 10 comments, still open.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4888)

2. **[#5019] Long-context tool loop crashes**  
   Repetitive identical tool calls terminate sessions with API error `Repetitive tool calls detected`. 4 comments, open, welcome for PR.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5019)

3. **[#5434] Extension marketplace misclassifies uppercase HTTP schemes**  
   `HTTPS://github.com/...` not recognized as GitHub source. Closed quickly.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5434)

4. **[#5518] Bundle restore rejects trailing separator paths**  
   Directory paths with trailing `/` break `restoreFiles()`. Closed.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5518)

5. **[#5562] CLI TUI: background rendering breaks on wrapped input lines**  
   Multi-line input shows terminal background instead of input background. 3 comments, closed.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5562)

6. **[#5555] `--resume` thinking block preview truncation**  
   Resume preview cuts off thinking blocks mid-content. 3 comments, closed.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5555)

7. **[#5559] Request: replayable fake model for no-AK tests**  
   Need fake OpenAI server for integration tests without API keys. 3 comments, open.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5559)

8. **[#5540] Request: revive completed background sub-agents**  
   Currently, completed sub-agents cannot receive messages again. 3 comments, open.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5540)

9. **[#5538] VS Code companion treats UNC paths as relative**  
   `\\server\share\file.ts` joined under workspace folder instead of opened directly. 3 comments, closed.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5538)

10. **[#5575] Chat upload adds random spaces to files**  
    Windows + Chrome upload introduces spaces like `fro m_secs`. 2 comments, closed (FAQ).  
    [Link](https://github.com/QwenLM/qwen-code/issues/5575)

## Key PR Progress

1. **[#5573] Always-on guard for consecutive identical tool calls**  
   Promotes loop detection from opt-in to always-on, halting runaway loops for all users.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5573)

2. **[#5557] Artifact tool for interactive HTML pages**  
   Adds experimental tool to publish and open self-contained HTML pages per session.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5557)

3. **[#5556] Revivable background sub-agents + TTL cleanup**  
   Completed sub-agents can receive new messages, with automatic transcript cleanup.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5556)

4. **[#5502] Voice dictation with native capture and streaming**  
   Hold/tap modes, silence detection, `/model --voice` for model selection.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5502)

5. **[#5560] Fake OpenAI server for no-AK integration tests**  
   Lightweight fixture-based test server enabling CI test runs without real API keys.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5560)

6. **[#5561] Live MCP server reconciliation on settings change**  
   Editing `mcpServers` in settings now hot-reloads without restart.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5561)

7. **[#5551] Release failure autofix workflow**  
   Failed releases now automatically create bug issues and dispatch autofix.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5551)

8. **[#5571] Enable loop detection by default**  
   Lowers duplicate threshold and enables it for all users (fixes #5019).  
   [Link](https://github.com/QwenLM/qwen-code/pull/5571)

9. **[#5030] Resume interrupted turn without synthetic "continue"**  
   First-class continuation for crashed or interrupted sessions.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5030)

10. **[#5003] TUI: remove tool group borders and collapse results**  
    Cleaner TUI by removing rounded borders and compacting completed tool outputs.  
    [Link](https://github.com/QwenLM/qwen-code/pull/5003)

## Feature Request Trends

- **Background automation**: Reviving completed sub-agents (#5540), autofix for release failures (#5549)
- **Voice & multimodal**: Voice dictation (#5502), vision bridge for text-only models (#5126)
- **CI/CD improvements**: Fake model servers for no-AK tests (#5559), integration tests on PR CI (#5219)
- **Plugin ecosystem**: Archive install sources for extensions (#4909), MCP live reload (#5561)
- **Terminal UX**: Project name/model display in TUI (#5546), artifact tool for HTML output (#5557)

## Developer Pain Points

- **Tool call loop crashes** — Long-context sessions crash due to repetitive tool calls; opt-in detection was off by default (#5019, #5571)
- **Windows path handling** — UNC paths misclassified as relative (#5538), absolute Windows paths treated as relative (#5522), trailing separators rejected (#5518)
- **CI blind spots** — Integration tests only run on release, so PR regressions go undetected (#5219)
- **Resume preview truncation** — Thinking blocks and history are clipped on `--resume` (#5555, #5566)
- **IDE plugin gaps** — question UI broken in IDEA (#4888), no automatic VS Code companion release after CLI release (#5570)

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-22

## Today's Highlights

The project has undergone a significant identity shift: **CodeWhale** is now the canonical name, replacing the legacy `deepseek-tui` npm package, with a formal rebranding guide published. The v0.8.64 release train is in full swing, with a major push toward security hardening, architectural refactoring, and reliability improvements. Community activity is high, with 35 open issues and 25 pull requests updated in the last 24 hours, reflecting both growing adoption and the challenges of scaling a complex TUI-based agentic coding tool.

---

## Releases

**v0.8.63** — Rebranding milestone: The project, command, npm package, and release assets are now uniformly named **CodeWhale**. The legacy `deepseek-tui` npm package is deprecated and will receive no further updates. Users migrating from v0.8.x should follow the instructions in `docs/REBRAND.md`.

---

## Hot Issues (10 noteworthy)

### 1. [#3368 — Security hardening/code-scanning fixes for v0.8.64](https://github.com/Hmbown/CodeWhale/issues/3368)
The release train’s public tracker for security-hardening work spanning CodeQL findings, advisory reports, and integration commits. 26 comments — the most active thread today. Critical for enterprise adoption.

### 2. [#2487 — Frequent "Turn stalled" error in yolo mode](https://github.com/Hmbown/CodeWhale/issues/2487)
Long-standing reliability bug (17 comments): `yolo` mode freezes with "no completion signal received." Continue commands don't resume. A top pain point for power users.

### 3. [#3144 — Natural-language auto-review policy and pre-push gate](https://github.com/Hmbown/CodeWhale/issues/3144)
Inspired by Cursor’s review gate. Proposes a configurable auto-review policy before code execution, with a pre-push gate. 12 comments — community enthusiastic about safety without sacrificing autonomy.

### 4. [#3275 — Overly involved modifications: self-questioning and deviating from intent](https://github.com/Hmbown/CodeWhale/issues/3275)
A regression from issue #3061. The agent enters self-driven loops of proposing and executing without user confirmation. 11 comments; users demand tighter intent adherence.

### 5. [#1812 — TUI freezes on Windows 11](https://github.com/Hmbown/CodeWhale/issues/1812)
Intermittent freezes on Windows — UI unresponsive but process alive. Captured with logs and thread-state analysis. 8 comments; cross-platform reliability remains a concern.

### 6. [#3222 — `reasoning_style` override for inline-tag thinking blocks](https://github.com/Hmbown/CodeWhale/issues/3222)
Parsing of reasoning content from MiniMax M3 is broken. Requests an override for OpenAI chat-completions providers. 6 comments; model diversity is a growing need.

### 7. [#3289 — UI freezes after auto-spawning multiple agents](https://github.com/Hmbown/CodeWhale/issues/3289)
v0.8.61 regression: plan mode spawns several sub-agents, then the UI freezes. 5 comments; multi-agent orchestration stability is fragile.

### 8. [#2608 — Refactor: extract provider registry from ballooning config files](https://github.com/Hmbown/CodeWhale/issues/2608)
`crates/config/src/lib.rs` is 4,719 lines; `crates/tui/src/config.rs` is 9,402 lines. Every new provider requires 15–30 match arms across both files. 4 comments; maintainability crisis recognized by maintainers.

### 9. [#3355 — Sandbox blocks Git write ops on worktree workspaces](https://github.com/Hmbown/CodeWhale/issues/3355)
Git worktrees can’t use the sandbox safely — `git add` fails unless trust mode is enabled. 3 comments; a sharp edge for developers using modern Git workflows.

### 10. [#3364 — Read-before-edit guardrails and clearer edit failures](https://github.com/Hmbown/CodeWhale/issues/3364)
Edit mistakes erode trust. Proposes forcing fresh reads before edits and making failures loud and specific. 1 comment but high impact for reliability.

---

## Key PR Progress (10 important)

### 1. [#3371 — fix(ui): reduce minimum terminal width for sidebar visibility](https://github.com/Hmbown/CodeWhale/pull/3371)
Fixes #3328: sidebar was hidden on terminals < 100 columns. Lowers the threshold for better accessibility on common terminal sizes.

### 2. [#3348 — fix(release): harden branch hygiene checks](https://github.com/Hmbown/CodeWhale/pull/3348)
Fixes #3214: improves release branch hygiene by adding `--remote` support for fork checkouts and fully qualifying remote refs.

### 3. [#3370 — feat(integrations): add WeCom (企业微信) intelligent robot bridge](https://github.com/Hmbown/CodeWhale/pull/3370)
New integration: bridges CodeWhale to WeCom (WeChat Work) for enterprise messaging. Broadens the platform’s reach into Chinese enterprise ecosystems.

### 4. [#3329 — fix(config): restore huggingface env precedence](https://github.com/Hmbown/CodeWhale/pull/3329)
Restores Hugging Face API key env variable precedence so the CI lint gate passes on `main`. A regression fix that unblocks CI.

### 5. [#3332 — fix(app-server): require auth for non-loopback binds](https://github.com/Hmbown/CodeWhale/pull/3332)
Fixes #3258: security hardening — rejects non-loopback app-server binds without explicit auth tokens. Critical for safe remote usage.

### 6. [#3356 — fix(tui): allow worktree git metadata writes in sandbox](https://github.com/Hmbown/CodeWhale/pull/3356)
Fixes #3355: detects Git worktree linked `.git` pointers and allows sandbox write access to the main repo’s git metadata directory.

### 7. [#3345 — refactor(config): move inline tests to module](https://github.com/Hmbown/CodeWhale/pull/3345)
Closes #3307: extracts config tests from `crates/config/src/lib.rs` into a separate `tests.rs` module, reducing production code bulk.

### 8. [#3333 — refactor(tui): split MCP header helpers](https://github.com/Hmbown/CodeWhale/pull/3333)
First step toward #3310: moves HTTP header framing helpers into `mcp::headers` submodule, making the MCP transport split easier to review.

### 9. [#3346 — style(clippy): fix clippy warnings](https://github.com/Hmbown/CodeWhale/pull/3346)
Runs `cargo clippy --fix` across the codebase. Housekeeping that reduces technical debt and improves code quality.

### 10. [#3344 — fix(tui): retry Codex responses requests](https://github.com/Hmbown/CodeWhale/pull/3344)
Fixes #3019: adds retry logic to the Codex Responses streaming path, rebuilding request body and headers per attempt. Improves reliability against transient failures.

---

## Feature Request Trends

1. **Architectural Refactoring – The Monolith Problem** (Issues #2608, #3306–#3314, #3345)
   A coordinated push to split the largest Rust files — config (9,402 lines), runtime API, MCP transports, UI event loop, `App` god object (150+ fields) — into focused modules. The maintainer is driving this methodically, with 8+ issues filed in the last 5 days alone.

2. **Agent Reliability & Intent Adherence** (Issues #2487, #3275, #3289, #3364)
   Models over-extending scope, freezing, or entering self-questioning loops. Users want read-before-edit guardrails, clearer failure signals, and tighter adherence to user intent — especially in `yolo` mode.

3. **Security & Governance** (Issues #3368, #3144, #3367)
   Auto-review policies, pre-push gates, subagent persona definitions, and sandbox improvements. Enterprise readiness is a clear priority.

4. **Provider/Model Diversity** (Issues #3222, #3357)
   Requests for MiniMax M3 reasoning support, Baidu Qianfan integration, and a `custom` provider flag. Users want to bring their own models without code changes.

5. **Context Management** (Issues #3363, #3366)
   Auto-compaction with carried-forward summaries, and consolidating overlapping work-tracking surfaces (plans, todos, tasks) into one canonical model-visible format.

6. **User-Defined Subagent Personas** (Issue #3367)
   Community wants `.codewhale/agents/` as a user-owned directory for reusable local agent personas, reducing dependency on built-in types.

---

## Developer Pain Points

- **Windows TUI Stability**: Intermittent freezes (#1812) and sub-agent UI deadlocks (#3289) erode trust on Windows platforms.
- **Config Monolith**: The 9,402-line `tui/src/config.rs` and 4,719-line `config/src/lib.rs` are a maintenance nightmare — every provider addition requires touching 15–30 match arms across both files (#2608).
- **Sandbox vs. Git Workflows**: The sandbox blocks Git operations on worktrees (#3355) and requires trust/YOLO mode, undermining security benefits.
- **"Turn Stalled" Error**: The most commented reliability bug (#2487) frustrates yolo-mode users; recovery is impossible without restarting.
- **Agent Over-Eagerness**: Models that self-question, self-answer, and deviate from user intent (#3275) waste context window and user patience.
- **Context Limits**: Long sessions hit token limits with no seamless auto-compaction, forcing manual wraps or restarts (#3363).
- **Non-English/Asian Model Support**: Broken reasoning parsing (#3222) and missing provider flags (#3357) show the tool is optimized primarily for flagship Western models.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*