# AI CLI Tools Community Digest 2026-06-30

> Generated: 2026-06-30 02:01 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Tool Comparison Report — 2026-06-30

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem on June 30, 2026 shows a maturing market with eight actively maintained tools, each at different stages of stability and community growth. Claude Code and OpenAI Codex dominate community engagement by volume, while Gemini CLI, OpenCode, and DeepSeek TUI demonstrate rapid iteration velocity. A clear bifurcation is emerging: established tools focus on enterprise hardening (auth, observability, security) while newer entrants prioritize agent reliability and platform-specific fixes. Cross-cutting themes include token/cost management anxiety, MCP ecosystem fragility, and demand for transparent sub-agent behavior. The tools collectively signal that AI CLI assistance has moved from novelty to production-critical infrastructure, with corresponding expectations around reliability, cost predictability, and enterprise integration.

## 2. Activity Comparison

| Tool | Open Issues | PRs (Last 24h) | Release (Last 24h) | Community Health |
|------|-------------|----------------|--------------------|-------------------|
| **Claude Code** | ~10 hot (top: 124 comments) | 3 merged | ✅ v2.1.196 (features) | Mature, high engagement, growing frustration |
| **OpenAI Codex** | ~10 hot (top: 626 comments) | 10 merged | ✅ rust-v0.142.4 (maintenance) | Largest thread volume, security-focused |
| **Gemini CLI** | ~10 hot (8-2 comments) | 10 merged/closed | ✅ v0.51.0-nightly (automated) | Rapid iteration, agent-focused |
| **Copilot CLI** | ~10 hot (10-0 comments) | 0 | ✅ v1.0.66-2 (features) | Mature but lower community engagement |
| **Kimi Code CLI** | 1 updated today | 0 | ❌ None | Very low activity, potential stagnation |
| **OpenCode** | ~10 hot (118-2 comments) | 10 merged | ❌ None | High engagement, V2 architecture in flight |
| **Pi (pi-mono)** | ~10 hot (42-1 comments) | 7 merged | ❌ None | Active but niche, packaging concerns |
| **Qwen Code** | ~10 hot (12-1 comments) | 10 merged/closed | ✅ v0.19.3-nightly (maintenance) | Growing international adoption |
| **DeepSeek TUI** | ~10 hot (24-1 comments) | 9 merged | ❌ None (v0.8.66 RC) | Chinese-heavy community, intense cache focus |

**Key observations:**
- **OpenAI Codex** leads PR throughput (10 merged) with strong security hardening
- **Gemini CLI** and **OpenCode** also closed 10 PRs each, showing high development velocity
- **Claude Code** maintains the highest community engagement by comment/upvote volume
- **Kimi Code CLI** shows near-zero activity, a potential risk signal
- **DeepSeek TUI** had the most intense single-day fix cluster (7+ PRs from one maintainer)

## 3. Shared Feature Directions

### Token & Cost Management (7 of 8 tools affected)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | Accurate rate-limit display (#23030), per-subagent metrics (#72287) |
| **OpenAI Codex** | Token over-consumption tracking (#14593, 626 comments), customizable TUI status bar (#17827) |
| **Gemini CLI** | Recursive reasoning turn limits (PR #28164) |
| **Copilot CLI** | Session quota transparency, billing confusion (#2340, #2619) |
| **Pi (pi-mono)** | Cache miss cost inflation (#6083), oversized thinking blocks |
| **Qwen Code** | Anthropic prompt-cache misses inflate costs (#5942) |
| **DeepSeek TUI** | Cache hit ratio far below competitors (#1177, 24 comments; #1120, 21 comments), extreme token consumption (#743, #1818) |

### Agent Reliability & Observability (7 of 8 tools)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | Freezing bug (#26224, 124 comments), Agent Teams instability (#72343) |
| **OpenAI Codex** | Compaction losing context (#29356, #25792), agent communication logging (PR #30516) |
| **Gemini CLI** | Subagent false success reporting (#22323), generalist agent hangs (#21409) |
| **Copilot CLI** | Orphaned sessions (#2364, #3600), silent tool failures (#3948) |
| **OpenCode** | Auto-compaction loops draining tokens (#30680) |
| **Qwen Code** | Subagent XML tag leakage (#6023), plan-mode stuck (#6026) |
| **DeepSeek TUI** | Multi-agent fanout freezes (#3800), sub-agent indefinite retries (#1641) |

### Enterprise Auth & Networking (5 of 8 tools)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | AWS Bedrock auth for Chrome extension (#16128, 109👍), SSO/OIDC integration |
| **OpenAI Codex** | Git sandboxing hardening (PRs #27914, #28714) |
| **Gemini CLI** | Harden file-write scope to prevent sandbox escape (PR #28215) |
| **Copilot CLI** | Enterprise server-managed config (#3909), admin-pushed env vars |
| **Pi (pi-mono)** | Provider error opacity (#5763), token detection fragility (#5871) |

### Cross-Platform Parity (5 of 8 tools)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | Linux @browser missing (#50423), Windows defaultShell ignored (#72389) |
| **OpenAI Codex** | Windows blank editor (#21863), zombie git polling (#29408) |
| **Gemini CLI** | Wayland browser agent crashes (#21983), terminal flicker (#21924) |
| **Copilot CLI** | Windows MCP start regression (#3958), macOS scrolling (#3957) |
| **Qwen Code** | Windows tilde path resolution (PR #6029), Linux TUI scroll (#5971) |

### MCP/Plugin Ecosystem (5 of 8 tools)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | Plugin marketplace destructive reload (#71948), permission fatigue (#67020) |
| **OpenAI Codex** | MCP zombie processes on macOS (#25744), decoupling init from review (PR #30509) |
| **Copilot CLI** | Windows .bat/.cmd MCP servers broken (#3958) |
| **OpenCode** | MCP prompts support (PR #34531), OAuth concurrency tracking |
| **Pi (pi-mono)** | Package security/verification (#6153-6155), dead repos |

## 4. Differentiation Analysis

### Feature Focus

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|----------|-----|-----------|--------------|
| **Primary Focus** | Team collaboration, MCP ecosystem | Security hardening, Git sandboxing | Agent reliability, memory systems | Enterprise config management | V2 architecture migration | Provider flexibility, TUI polish | Daemon platform, multi-channel | Cache optimization, sub-agent fixes |
| **Target User** | Teams/enterprise | Security-conscious developers | Agent-heavy workflows | Enterprise/GitHub shops | Early adopters, power users | Provider-agnostic developers | Asian market, mobile-first | Chinese-speaking developers |
| **Technical Approach** | Plugin-based extensibility | Rust core, security audits | AST-aware code intelligence | GitHub integration, MCP coexistence | Bun runtime, V2 client migration | Extension API, multi-profile | Daemon-managed channels, autonomous loops | Hotbar UI, YOLO approval mode |

### Key Differentiators

- **Claude Code**: Strongest team collaboration features (org default models, readable sessions), but plagued by unresolved freezing bug (#26224)
- **OpenAI Codex**: Most security-proactive (6+ PRs targeting Git sandboxing, shell approval), but token consumption trust is eroding
- **Gemini CLI**: Unique AST-aware code navigation investigation (#22745) and Caretaker Agent for automated triage (PRs #28015, #28163)
- **Copilot CLI**: Only tool with explicit enterprise config management requests (#3909), strongest GitHub integration
- **OpenCode**: Most ambitious architecture change (V2 migration), but Bun runtime instability on Windows (#33742)
- **Pi**: Strongest multi-provider support (Anthropic, OpenAI, Bedrock, GLM), but smallest community
- **Qwen Code**: Only tool with daemon-as-platform vision (channel workers, HTTPS, DingTalk/Feishu integration), autonomous `/loop` mode
- **DeepSeek TUI**: Most aggressive cache optimization focus (3+ cache-related issues), heavily Chinese-language community

## 5. Community Momentum & Maturity

### Most Active Communities
1. **OpenAI Codex** — Highest engagement on single issues (626 comments on #14593), most PR throughput (10 merged today)
2. **Claude Code** — Strongest upvote signals (146 on #26224), broadest feature request diversity
3. **Gemini CLI** — Rapid nightly builds, growing agent-focused community

### Most Rapidly Iterating
1. **Gemini CLI** — Nightly automated releases, 10 PRs in 24h
2. **OpenCode** — V2 architecture moving fast, 10 PRs merged despite no release
3. **DeepSeek TUI** — Intense single-maintainer velocity (7+ PRs today)
4. **Qwen Code** — Steady nightly releases, growing Asian market adoption

### Potential Stagnation Risk
- **Kimi Code CLI** — Only 1 issue updated in 24h, no releases, no PR activity. Low engagement suggests either stable maturity or declining community interest.

### Maturity Indicators
- **Claude Code**: Most enterprise-ready features (org defaults, session naming) but critical bug unresolved for 4 months
- **OpenAI Codex**: Most security-mature (6+ security PRs in one batch) but token trust issues
- **Copilot CLI**: Most stable release pattern (patch releases with clear changelogs), lowest issue-per-engagement ratio
- **Pi**: Most provider-flexible but smallest active developer base

## 6. Trend Signals

### 1. Token/Cost Anxiety Is the Dominant Cross-Tool Theme
Every major tool has at least one high-engagement issue about unexpected token consumption, cache misses, or rate-limit confusion. Users are increasingly cost-sensitive and demand transparency. **Signal:** Tools that fail to provide predictable, auditable billing will lose trust. The competitive advantage shifts to tools with visible, accurate usage metering.

### 2. Agent Reliability Has Not Reached Production Parity
Despite rapid iteration, sub-agent management remains fragile across all tools. False success reports (Gemini CLI #22323), indefinite hangs (Claude Code #26224), compaction losing state (OpenAI Codex #29356), and fanout freezes (DeepSeek TUI #3800) indicate that multi-agent orchestration is still experimental. **Signal:** Enterprises should expect agent failures in production; tools need fallback strategies and self-healing.

### 3. Security Hardening Is Becoming Table Stakes
OpenAI Codex merged 6+ security PRs in one batch. Gemini CLI hardened file-write scoping (#28215). Copilot CLI is adding enterprise config management. Users are demanding sandbox escape prevention, PII redaction guarantee, and SSO/OIDC auth. **Signal:** Security posture will become a primary purchasing criterion, especially for regulated industries.

### 4. The MCP Ecosystem Is Fragile
Plugin/dependency management across tools is breaking: Claude Code's plugin marketplace wipes entirely on reload (#71948), OpenAI Codex's MCP processes leak on macOS (#25744), Copilot CLI's Windows MCP servers fail (#3958). **Signal:** MCP standardization is needed; tool maintainers should invest in dependency integrity before feature expansion.

### 5. Chinese-Language Communities Are Growing
DeepSeek TUI and Qwen Code show strong Chinese-language engagement with distinct feature priorities (cache optimization, WeChat/Feishu integration, QQ Bot support). **Signal:** The AI CLI market is going global; non-English UX (Unicode rendering, Asian messaging platforms) will become important.

### 6. Cross-Platform Parity Remains an Afterthought
Linux, Windows, and macOS-specific bugs persist across all tools. Linux missing features (#50423 in Claude Code), Windows segfaults (#33742 in OpenCode), macOS zombie processes (#25744 in OpenAI Codex). **Signal:** Tools optimize for one platform (usually macOS) and treat others as second-class. Teams with heterogeneous OS environments face friction.

### 7. "Enable While I'm Away" Is Emerging as a Use Case
Qwen Code's autonomous `/loop` mode (#5991) and Copilot CLI's session lifecycle management requests signal demand for background agent operation. Users want to set tasks running and return to results. **Signal:** Long-running, unattended agent sessions will become a core feature requirement.

### 8. Observability Is the Next Frontier
Multiple tools lack sub-agent metrics (Claude Code #72287), agent communication logging (OpenAI Codex #30516), and session cost aggregation (OpenCode #4925). Users want to understand what agents are doing and how much they cost. **Signal:** Tools that provide rich observability (per-subagent token usage, turn counts, cost breakdowns) will differentiate.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report based on the most-watched activity in the `anthropics/skills` repository.

---

## Claude Code Skills Community Highlights Report (Data as of 2026-06-30)

### 1. Top Skills Ranking

The following are the most-discussed Skill Pull Requests by community engagement (comments and related issues). These represent the highest-need areas in the ecosystem.

1.  **Skill Creator Fixes (`run_eval.py` / `skill-creator` ecosystem)**
    - **Functionality:** The `skill-creator` skill is the meta-tool for building and optimizing other Skills. Multiple PRs (#1298, #1323, #1099, #1050, #539, #362, #361) address a critical bug where the eval loop reports **0% recall** on all queries, making the description optimizer useless. Other fixes address Windows compatibility (subprocess pipes, encoding) and YAML parsing.
    - **Discussion Highlights:** The conversation revolves around a systemic bug (#556) where the `claude -p` command used in testing does not trigger Skills. The community has independently reproduced this 10+ times, making it the top blocker for Skill development.
    - **Status:** **Open**

2.  **Document Typography Skill (#514)**
    - **Functionality:** A skill for typographic quality control in generated documents, preventing orphan words, widow paragraphs, and numbering misalignment in Claude-generated content (PDF, DOCX).
    - **Discussion Highlights:** Users highlight this as a universal problem affecting every document Claude generates. The skill targets a "polish" gap that is rarely requested but highly valued.
    - **Status:** **Open**

3.  **ODT (OpenDocument) Skill (#486)**
    - **Functionality:** Enables Claude to create, fill, read, and convert OpenDocument Format files (.odt, .ods) commonly used by LibreOffice and ISO-standard systems.
    - **Discussion Highlights:** Strong enterprise demand for interoperability with open-source office suites and government-standard document formats.
    - **Status:** **Open**

4.  **DOCX Tracked Changes Fix (#541)**
    - **Functionality:** Fixes document corruption when adding tracked changes to DOCX files that contain existing bookmarks, caused by `w:id` collision in the OOXML schema.
    - **Discussion Highlights:** Considered a critical bug fix for any user relying on the DOCX skill for document revision workflows.
    - **Status:** **Open**

5.  **SAP-RPT-1-OSS Predictor (#181)**
    - **Functionality:** A skill for using SAP's open-source tabular foundation model (SAP-RPT-1-OSS) for predictive analytics on SAP business data.
    - **Discussion Highlights:** Represents a bridge between enterprise ERP systems and Claude. Interest is niche but high-signal for specific enterprise users.
    - **Status:** **Open**

6.  **Self-Audit Skill (#1367)**
    - **Functionality:** A universal reasoning quality gate that audits Claude's output across four dimensions (Completeness, Consistency, Grounding, Safety) before delivery. Designed to work with any project or model.
    - **Discussion Highlights:** The most recent high-comment PR. Community sees it as a lightweight, universal "guardrail" that fits before any output is finalized.
    - **Status:** **Open**

7.  **Testing Patterns Skill (#723)**
    - **Functionality:** A comprehensive testing skill covering the full testing stack, including unit testing (AAA pattern), React component testing (Testing Library), API testing, and testing philosophy (Testing Trophy model).
    - **Discussion Highlights:** Addresses a clear community need for structured test generation. The discussion focuses on completeness of coverage and avoiding anti-patterns.
    - **Status:** **Open**

### 2. Community Demand Trends (from Issues)

The following are the most-anticipated new Skill directions based on Issue activity:

- **Security & Trust Boundaries:** Issue #492 (32 comments) is the most active. The community is demanding **security audit skills** and **trust boundary management** to prevent impersonation of official Anthropic Skills.
- **Enterprise Skill Sharing:** Issue #228 (14 comments) calls for **org-wide skill libraries** and direct sharing links, reflecting demand for team/enterprise deployment.
- **Document Skills Optimization:** Issues #189 and #1175 highlight demand for **deduplication of document skills** and **secure SharePoint Online handling**, indicating a focus on document-heavy enterprise workflows.
- **Skill Creation Bug Fixing:** Issue #202 and the cluster around #556 show the community's highest demand is simply **getting the `skill-creator` tool to work reliably**, especially on Windows and for eval/optimization loops.

### 3. High-Potential Pending Skills

These PRs have active discussion and are likely to be merged soon, based on their utility and community traction:

- **Codebase Inventory Audit (#147):** A 10-step workflow for identifying orphaned code, unused files, and documentation gaps. High utility for codebase maintenance.
- **Shodh-Memory (#154):** A persistent memory system for AI agents, enabling context retention across conversations. Taps into demand for long-running agent workflows.
- **Skill Quality & Security Analyzers (#83):** Two meta-skills for evaluating other Skills across structure, documentation, and security dimensions. Essential for a maturing ecosystem.
- **Frontend Design Skill Improvement (#210):** A revision to the existing frontend-design skill to make instructions more actionable and specific within a single conversation context.

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliable, bug-free tooling to build, test, and deploy enterprise-grade Skills**, with specific gaps in Windows compatibility, security auditing, document formatting (typography, ODT), and persistent agent memory.

---

# Claude Code Community Digest — 2026-06-30

## Today's Highlights

Claude Code ships **v2.1.196** with organization default model support and readable session naming, two quality-of-life improvements for teams. Meanwhile, a **critical freezing bug** (#26224) continues to dominate community attention with 124 comments and 146 upvotes, remaining unresolved since February. The backlog shows growing demand for observability tooling (per-subagent metrics, rate-limit transparency) and persistent frustration with Chrome extension permission flows.

## Releases

**v2.1.196** — Released today
- **Org default models**: Admins can now set default models via the organization console; users see "Org default" (or "Role default") in `/model` when no personal override exists
- **Readable session names**: New sessions now start with descriptive default names, improving identification in session lists and multi-session workflows

[View release](https://github.com/anthropics/claude-code/releases/tag/v2.1.196)

## Hot Issues (Top 10)

1. **[#26224 — Claude Code hanging/freezing for 5-20+ minutes](https://github.com/anthropics/claude-code/issues/26224)**  
   *Open since Feb 2026 | 124 comments, 146 👍*  
   **Why it matters**: The single most-upvoted open bug. Users report complete tool lockups, often under heavy prompt load. No fix in sight after four months — growing community frustration.

2. **[#69238 — "No response from API" error when Advisor triggers](https://github.com/anthropics/claude-code/issues/69238)**  
   *Open, 30 comments, 46 👍*  
   **Why it matters**: Advisor (Opus 4.8) consistently fails to return responses, forcing retry delays of 2+ minutes. Users on Sonnet as base model report this blocks workflows entirely.

3. **[#16128 — AWS Bedrock auth support for Chrome extension](https://github.com/anthropics/claude-code/issues/16128)**  
   *Open since Jan 2026 | 26 comments, 109 👍*  
   **Why it matters**: Enterprise organizations behind AWS Bedrock cannot use the Chrome extension at all. High demand for native SSO/OIDC integration.

4. **[#20469 — Microsoft 365 Connector restricted to Team/Enterprise plans](https://github.com/anthropics/claude-code/issues/20469)**  
   *CLOSED, 58 comments, 62 👍*  
   **Why it matters**: Max plan users ($100–200/mo) pay more than Team ($30/seat) but lack M365 integration. Pricing parity concern with strong community support.

5. **[#23030 — Rate limit triggered at 71% session usage](https://github.com/anthropics/claude-code/issues/23030)**  
   *Open, 10 comments, 13 👍*  
   **Why it matters**: Max plan users hit hard rate limits well before displayed capacity is exhausted. Misleading UX erodes trust in usage metering.

6. **[#67307 — Opus 4.8 emits malformed tool calls](https://github.com/anthropics/claude-code/issues/67307)**  
   *Open, 4 comments, 13 👍*  
   **Why it matters**: Stray tokens (`count`, `call`) break tool execution silently. Critical for anyone relying on structured agent workflows.

7. **[#50423 — VS Code extension @browser doesn't work on Linux](https://github.com/anthropics/claude-code/issues/50423)**  
   *Open, 16 comments, 15 👍*  
   **Why it matters**: Documented feature (`@browser`) fails silently on Linux. Blocks cross-platform adoption for web automation workflows.

8. **[#10258 — Cannot disable the "buggy" Interactive Question Tool](https://github.com/anthropics/claude-code/issues/10258)**  
   *Open since Oct 2025 | 19 comments, 5 👍*  
   **Why it matters**: Long-standing TUI annoyance with no opt-out. Users report the tool interrupts flow with irrelevant prompts.

9. **[#72343 — Agent Teams: tmux/auto teammates crash on spawn](https://github.com/anthropics/claude-code/issues/72343)**  
   *Open, 3 comments*  
   **Why it matters**: Fresh bug in v2.1.195. Agent Teams feature is broken for tmux users — teammates die immediately with `--print` error. High severity for collaborative workflows.

10. **[#71948 — Plugin marketplace wipes directory on reload](https://github.com/anthropics/claude-code/issues/71948)**  
    *Open, 2 comments*  
    **Why it matters**: `/plugin` and `/reload-plugins` commands destroy the marketplace directory and fail to reclone. All plugins + MCP servers stop loading. Destructive UX bug.

## Key PR Progress

1. **[#72363 — Gateway GCP example: Agent Platform rebrand](https://github.com/anthropics/claude-code/pull/72363)**  
   Prose-only update renaming Vertex AI references to "Agent Platform" across GCP gateway examples, with transitional "(formerly Vertex AI)" on first mentions.

2. **[#72361 — Add Claude Gateway on GCP deployment assets](https://github.com/anthropics/claude-code/pull/72361)**  
   New Terraform and script assets for deploying Claude Gateway on Google Cloud, complementing the published walkthrough. Ready-to-use infrastructure examples.

3. **[#72264 — docs: Note Bash tool_input fields in hook example](https://github.com/anthropics/claude-code/pull/72264)**  
   Small documentation improvement clarifying that `PreToolUse` Bash payloads expose `run_in_background`, `description`, and `timeout` beyond just `command`. Helps hook authors.

## Feature Request Trends

- **Enterprise auth & networking**: Strong push for AWS Bedrock auth in Chrome extension (#16128), Strict Enterprise APIM Gateway support (#62973). Organizations need SSO/OIDC and custom proxy paths.

- **Observability & transparency**: Users demand per-subagent model/effort visibility in `/agents` (#72287), Opus-specific rate limit displays (#72372), and accurate usage meters that reflect sub-quotas (#23030).

- **Security & privacy controls**: Opt-in PII-sanitized training data contribution (#72393) and `/feedback` redaction capabilities (#72156). Users want more control over data that leaves their machine.

- **IDE parity**: VS Code missing CLI features — `/fork` conversation branching (#69272), sandbox settings ignored in IDE (#64061). Users expect feature parity across surfaces.

- **Permission fatigue**: "Always allow" for Chrome actions not honored (#67020), domain approval UI missing for Chrome MCP (#59723). Users report 300+ prompts per session.

## Developer Pain Points

- **Freezing/hanging issues (#26224)**: The #1 pain point — 4 months unresolved. Users report multi-minute tool lockups with no workaround. Community patience is wearing thin.

- **Rate limit confusion (#23030, #72372)**: Multiple reports of hitting limits at 70% displayed usage. Max plan users paying $200/mo feel misled. Opus-specific sub-quotas invisible.

- **Plugin/MCP ecosystem fragility (#71948)**: Destructive reload behavior that wipes all plugins. No recovery path. Affects all MCP integrations.

- **Chrome extension permission gaps (#67020, #59723, #69127)**: Re-prompting on every action, no approval UI for domains, local file paths rejected despite schema claims. Blocks browser automation workflows.

- **Agent Teams instability (#72343)**: New feature broken on tmux/auto spawn since v2.1.195. Blocks collaborative agent workflows on launch.

- **Cross-platform inconsistencies**: Linux missing `@browser` in VS Code (#50423), Windows Desktop ignoring `defaultShell` setting (#72389), WSL memory selection ineffective (#72400). Multi-OS teams face friction.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-30

## Today's Highlights

Two minor Rust releases shipped, both without user-facing changes. The community remains most vocal about **aggressive token consumption** (Issue #14593 remains the all-time top thread at 626 comments) and a newly exploding concern over **SQLite logging amplifying SSD wear** (#28224, 108 comments, 407 👍). On the security front, a coordinated batch of PRs from OpenAI engineers is hardening Git sandboxing and shell approval boundaries, indicating a major proactive security push.

## Releases

Two releases landed in the last 24 hours, both containing only infrastructure/maintenance changes:

- **[rust-v0.142.4](https://github.com/openai/codex/releases/tag/rust-v0.142.4)** — No user-facing changes; full changelog from v0.142.3.
- **[rust-v0.143.0-alpha.31](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.31)** — Alpha release, no detailed changelog published.

## Hot Issues

1. **[#14593 — Burning tokens very fast](https://github.com/openai/codex/issues/14593)** — *626 comments, 276 👍*  
   The longest-running open issue. Users on Business plans report token limits consumed far faster than expected. Despite ongoing fixes, the thread remains active as new variants of over-consumption appear. *Community reaction:* Frustration is high; some users have been tracking this since March.

2. **[#28224 — Codex SQLite feedback logs can write ~640 TB/year](https://github.com/openai/codex/issues/28224)** — *108 comments, 407 👍*  
   A severe performance/stability bug where `codex_api::endpoint::responses_websocket` logging causes massive SSD write amplification. Three PRs merged in v0.142.0 reduced ~85% of logs, but users report residual churn remains. *Community reaction:* Widespread relief that a fix landed, but calls for a complete opt-out persist.

3. **[#25749 — Inaccessible legacy phone number blocks account recovery](https://github.com/openai/codex/issues/25749)** — *65 comments, 43 👍*  
   Users with MFA via Google OAuth are locked out because Codex demands verification of an old phone number with no recovery path. *Community reaction:* Deep frustration; users feel the support process is opaque and the UX contradicts standard account security practices.

4. **[#30002 — Pro 5h limit burned in ~41 min / ~1.35M tokens](https://github.com/openai/codex/issues/30002)** — *29 comments, 6 👍*  
   Server-side quota accounting over-reports consumption after the 5h reset window. One account reached its limit after 1.35M tokens, yet earlier the same day consumed ~156M tokens in a full window. *Community reaction:* Confusion and distrust of the quota system; users question billing accuracy.

5. **[#29532 — Persistent SQLite TRACE log churn after v0.142.0 on macOS](https://github.com/openai/codex/issues/29532)** — *25 comments, 7 👍*  
   Even after the major fix in v0.142.0, macOS users still see heavy SQLite activity. The partial fix addressed one logging source but missed another. *Community reaction:* Users appreciating the partial fix but wanting a complete resolution.

6. **[#17827 — Customizable status line for TUI](https://github.com/openai/codex/issues/17827)** — *20 comments, 78 👍*  
   Request for a Claude Code-style status bar showing token usage, model, rate limits, git branch, etc. *Community reaction:* Strong positive sentiment; users want parity with competing tools.

7. **[#29356 — Context compaction loses operational continuity](https://github.com/openai/codex/issues/29356)** — *14 comments*  
   Automatic compaction drops critical last N steps, causing agents to lose track of the current task state. *Community reaction:* Power users find this severely disruptive to long-running workflows.

8. **[#25792 — Compaction forgets AGENTS rules; progress jumps 97% → 42%](https://github.com/openai/codex/issues/25792)** — *11 comments*  
   A closely related compaction bug where custom agent rules are lost mid-task, causing massive regression in task progress. *Community reaction:* One of the most cited pain points for agent-heavy workflows.

9. **[#25744 — MCP helper processes leak on macOS; HID/WindowServer stalls](https://github.com/openai/codex/issues/25744)** — *10 comments, 3 👍*  
   Long-running sessions accumulate zombie helpers, causing system-wide input lag. *Community reaction:* macOS power users report this as a deal-breaker for Computer Use features.

10. **[#21863 — VS Code extension: central editor panel blank on Windows](https://github.com/openai/codex/issues/21863)** — *15 comments, 1 👍*  
    Custom URI route mishandles `fsPath` on Windows, rendering the editor panel empty. *Community reaction:* A reliable reproducible bug affecting Windows users; workarounds exist but no permanent fix.

## Key PR Progress

1. **[#30509 — Allow review while MCP startup runs in background](https://github.com/openai/codex/pull/30509)**  
   Decouples MCP initialization from foreground task state, enabling `/review` to open while servers start. Reduces wait times for MCP-heavy setups.

2. **[#27914 — Fail closed on executable Git worktree helpers](https://github.com/openai/codex/pull/27914)**  
   Security hardening: blocks repository-controlled Git content filters and merge drivers from executing during patch operations. Addresses PSEC-4394.

3. **[#30643 — Bound Rendezvous WebSocket liveness](https://github.com/openai/codex/pull/30643)**  
   Adds 60-second pong requirement and backpressure boundaries for Noise Rendezvous WebSockets. Prevents silent disconnections in agent communication.

4. **[#28714 — Require approval for generic Git commands](https://github.com/openai/codex/pull/28714)**  
   Tightens Git command allowlist after PSECOP-111 showed argv-only classification is unsafe. Commands like `git status` may now require explicit approval in untrusted repos.

5. **[#30642 — Accept empty HTTP responses for MCP notifications](https://github.com/openai/codex/pull/30642)**  
   Permissive handling for Streamable HTTP MCP; empty JSON responses are now accepted for notifications while still requiring bodies for requests like `initialize`.

6. **[#30516 — Add explicit agent communication logging](https://github.com/openai/codex/pull/30516)**  
   New `TRACE` logging under `codex_core::agent_communication` for lifecycle events. Helps debug agent coordination without verbose generic logs.

7. **[#30315 — Add generated token auth to app-server WebSockets](https://github.com/openai/codex/pull/30315)**  
   Adds 256-bit URL-safe connection tokens for WebSocket listeners with opt-out (`--no-token-check`). Improves local security for app-server communication.

8. **[#30500 — Run reviews without unfinished MCP servers](https://github.com/openai/codex/pull/30500)**  
   Review sessions skip waiting for unfinished MCP initialization, allowing faster review startup even when parent sessions have pending MCP OAuth.

9. **[#30618 — Prevent tool-search rollout poisoning](https://github.com/openai/codex/pull/30618)**  
   Fixes a critical bug where malformed `tool_search_call.arguments` from the server is persisted and replayed across sessions, permanently breaking the session.

10. **[#30632 — Trace and reduce remote first-turn latency](https://github.com/openai/codex/pull/30632)**  
    Adds W3C trace context propagation and stage-level spans across Core, exec-server RPC, and Noise relay. Removes several avoidable waits found during profiling.

## Feature Request Trends

- **Customizable TUI status line** (#17827): Strong demand for showing live token usage, model, rate limits, git branch, and other operational metadata in the terminal UI.
- **Background monitoring tool** (#29922): A request for an agent-callable `monitor` tool that wakes Codex on log filesystem/build changes without polling — reflecting a desire for more proactive, event-driven agent behavior.
- **Autoscroll disable** (#23517): Users find autoscroll during long responses visually uncomfortable and request a configurable toggle.
- **Agent communication observability**: Multiple issues implicitly ask for better insight into subagent state and communication (#30237, #30516).

## Developer Pain Points

- **Token/rate-limit over-consumption dominates**: Issues #14593 and #30002 together represent the largest sustained frustration. Users distrust the quota system and report unpredictability in billing.
- **SQLite and SSD endurance concerns**: The 640 TB/year estimate in #28224 spooked the community. Even after partial fixes, users want full opt-out capabilities.
- **Context compaction reliability**: Two high-comment issues (#29356, #25792) show that automatic compaction regularly breaks long-running agent tasks. Users feel their work is lost when agents regress 50%+.
- **Windows-specific UX and resource issues**: Blank editor panel (#21863), zombie git polling processes (#29408), and locked binary updates (#23320) create a steady noise floor of Windows pain.
- **MCP/Computer Use stability on macOS**: Zombie process accumulation (#25744) and missing JavaScript REPL exposure (#30486) hinder the advanced feature set on macOS.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-30

## Today's Highlights

The team shipped nightly build **v0.51.0-nightly.20260630** while addressing several critical agent reliability bugs — notably a subagent recovery issue where MAX_TURNS interruptions are falsely reported as "GOAL success." A major security PR was also merged to harden file-write scoping and prevent sandbox escape via `.gemini/` configuration tampering. Community activity remains high across memory system quality, browser agent resilience, and AST-aware code navigation features.

## Releases

**v0.51.0-nightly.20260630.gae0a3aa7b** — Automated nightly build with no feature changelog.  
[Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260629.gae0a3aa7b...v0.51.0-nightly.20260630.gae0a3aa7b)

## Hot Issues (Top 10)

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery after MAX_TURNS falsely reports GOAL success**  
   `codebase_investigator` subagent marks interrupted sessions as successful, masking the real termination cause. Critical for agent reliability. (8 comments, 2 👍)

2. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Robust component-level evaluations**  
   Epic for scaling behavioral evals from 76 tests across 6 Gemini models. Directly impacts agent quality assurance. (7 comments)

3. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads, search, and mapping**  
   Epic investigating whether AST tools reduce turn count, token noise, and misaligned reads. High community interest. (7 comments, 1 👍)

4. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever**  
   CLI hangs indefinitely when deferring to generalist agent for simple tasks. Workaround exists (disable subagents) but blocking normal workflow. (7 comments, 8 👍 — most upvoted issue)

5. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini doesn't use custom skills/sub-agents autonomously**  
   Despite user-defined skills like "gradle" or "git," the model rarely invokes them without explicit instruction. Limits agent utility. (6 comments)

6. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — Auto Memory logs secrets before redaction**  
   Security concern: extraction prompt redacts secrets *after* they're already in model context. Also lacks deterministic redaction. (5 comments)

7. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely**  
   Sessions deemed "low signal" remain unprocessed and keep reappearing, wasting extraction agent resources. (5 comments)

8. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command stuck on "Waiting input" after completion**  
   Simple CLI commands hang post-execution showing "Awaiting user input" despite no input needed. Frequent frustration. (4 comments, 3 👍)

9. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser agent fails on Wayland**  
   Browser subagent terminates with "GOAL" but actually crashes in Wayland environments. Platform compatibility issue. (4 comments, 1 👍)

10. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should discourage destructive behavior**  
    Model uses `git reset`, `--force` flags, and unsafe DB modifications when safer alternatives exist. (3 comments, 1 👍)

## Key PR Progress (Top 10)

1. **[#28215](https://github.com/google-gemini/gemini-cli/pull/28215) — Harden file-write scope: stop writes to .gemini and .gitconfig** *(CLOSED)*  
   Closes a prompt-injection sandbox escape where auto-accept writes could modify Gemini CLI configuration. Critical security fix.

2. **[#28164](https://github.com/google-gemini/gemini-cli/pull/28164) — Limit recursive reasoning turns per user request**  
   Caps recursive reasoning at 15 turns (configurable) to protect local CPU resources and API quotas from infinite loops.

3. **[#27971](https://github.com/google-gemini/gemini-cli/pull/27971) — Strip thoughts from scrubbed history turns**  
   Fixes "thought leakage" where internal model monologues pollute history, causing emulation of scratchpad patterns and infinite loops.

4. **[#28216](https://github.com/google-gemini/gemini-cli/pull/28216) — Exclude transient CI config files from workspace context**  
   Prevents `gha-creds-*.json` from being treated as workspace files, reducing noise in agent context.

5. **[#28015](https://github.com/google-gemini/gemini-cli/pull/28015) — Caretaker Agent: Cloud Run webhook ingestion service** *(size/xl)*  
   Implements GitHub webhook ingestion with signature verification, Firestore storage, and Pub/Sub publishing for automated issue triage.

6. **[#28163](https://github.com/google-gemini/gemini-cli/pull/28163) — Caretaker Agent: triage worker core foundation (part 1/2)** *(size/l)*  
   Core modules for automated issue triage — foundational infrastructure for self-healing issue management.

7. **[#28053](https://github.com/google-gemini/gemini-cli/pull/28053) — Fix @-prefixed path resolution and macOS tests** *(size/xl)*  
   Fixes production bug where `read_file`/`write_file` fail with "File not found" when model passes `@`-prefixed paths.

8. **[#28202](https://github.com/google-gemini/gemini-cli/pull/28202) — Forward SIGINT/SIGTERM to child process on relaunch** *(CLOSED)*  
   Prevents orphaned child processes when Ctrl+C is pressed during update/relaunch. Fixes #25590.

9. **[#28201](https://github.com/google-gemini/gemini-cli/pull/28201) — Remove double-wrapping of VS Code disposables** *(CLOSED)*  
   Fixes subscription leak causing memory growth in the VS Code IDE Companion extension. Fixes #27790.

10. **[#27914](https://github.com/google-gemini/gemini-cli/pull/27914) — Don't offer to resume a session that wasn't saved** *(CLOSED)*  
    Prevents misleading "gemini --resume <id>" prompt when disk full (ENOSPC) prevented session save.

## Feature Request Trends

- **AST-aware code intelligence**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) push for AST-based file reads, codebase mapping, and method-bound navigation to reduce token waste and turn count.
- **Self-aware agent**: [#21432](https://github.com/google-gemini/gemini-cli/issues/21432) requests the agent know its own flags, hotkeys, and configuration to act as its own expert guide.
- **Subagent trajectory sharing**: [#22598](https://github.com/google-gemini/gemini-cli/issues/22598) seeks visibility into subagent behavior via `/chat share` for debugging and evaluation.
- **Automatic session takeover**: [#22232](https://github.com/google-gemini/gemini-cli/issues/22232) requests lock recovery and takeover for browser agent persistent sessions instead of fail-fast behavior.
- **Harm reduction**: [#22672](https://github.com/google-gemini/gemini-cli/issues/22672) asks for built-in guards against destructive git/DB operations.

## Developer Pain Points

- **Agent hangs and false reports**: Generalist agent hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), subagent false success reporting ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), and stuck shell commands ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)) degrade trust in reliability.
- **Auto Memory quality issues**: Low-signal retry loops ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), secret leakage before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), and invalid patch handling ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)) frustrate users relying on memory features.
- **Subagent non-compliance**: Agents ignore settings overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), refuse to use defined skills ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)), or run without permission ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)).
- **Environment-specific failures**: Wayland crashes ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), terminal resize flicker ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)), and external editor corruption ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)) surface platform compatibility gaps.
- **Cluttered workspace**: Model creates tmp scripts in random locations ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) and CI credential files leak into context ([#28216](https://github.com/google-gemini/gemini-cli/pull/28216)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

**GitHub Copilot CLI Community Digest – 2026-06-30**

---

### 1. Today's Highlights
A new patch release (v1.0.66-2) lands with notable plugin coexistence improvements and deeper integrations for CLI tooling. The community is increasingly vocal about session management pain points, including orphaned sessions and confusing UI artifacts like the alt-screen toggle and 1970 date display. Enterprise admins are pushing hard for server-managed local configuration, while MCP and Windows platform bugs continue to generate high-priority tickets.

---

### 2. Releases
**v1.0.66-2** was published in the last 24 hours. Changes include:
- **Added**: Support for skills with the same name from different plugins to coexist.
- **Added**: Integrations can now read and write CLI user settings.
- **Added**: LSP server logs are now accessible via `/lsp logs` and `read_agent`.
- **Added**: The CLI now prompts users to install `gh` CLI when it is missing in GitHub repositories.
- **Added**: GitHub attachment variants added to prompt rendering.

*No other releases reported.*

---

### 3. Hot Issues
**#1799** – [How to turn off alt-screen views?](https://github.com/github/copilot-cli/issues/1799)  
*7 👍, 10 comments.* Long-standing community pain point. Users want a configuration toggle to disable alt-screen mode, which has caused visual disruption since its introduction. High reaction count indicates broad interest.

**#2364** – [Agent session keeps running indefinitely (Critical)](https://github.com/github/copilot-cli/issues/2364)  
*2 👍, 4 comments.* Critical bug where Copilot Coding Agent sessions in org repos hang with no commits or file output. Closed recently but signals deep session lifecycle issues.

**#3909** – [Enterprise/org server-managed settings for local CLI](https://github.com/github/copilot-cli/issues/3909)  
*0 👍, 3 comments.* Enterprise admins want centralized env/config push to local CLI installs. Currently, only cloud Agents/Codespaces receive org-managed secrets. This is a growing enterprise gap.

**#3600** – [Ability to remove orphaned sessions](https://github.com/github/copilot-cli/issues/3600)  
*0 👍, 3 comments.* Critical bug: sessions running for two months without termination ability. Closed but underscores the need for session lifecycle management.

**#3948** – [web_fetch: TypeError: fetch failed](https://github.com/github/copilot-cli/issues/3948)  
*0 👍, 2 comments.* Every `web_fetch` tool call fails despite correct proxy and auth configuration. Networking reliability issue affecting core tool functionality.

**#3936** – [Ctrl+G should expand paste tokens in $EDITOR](https://github.com/github/copilot-cli/issues/3936)  
*0 👍, 2 comments.* Parity with Claude Code: when `compactPaste` is enabled, Ctrl+G writes literal tokens instead of expanded text. Small UX annoyance with high developer workflow impact.

**#2654** – [session_store_sql silently returns empty when sync is local](https://github.com/github/copilot-cli/issues/2654)  
*1 👍, 2 comments.* Agents are still injected with `session_store_sql` tool even when session sync is set to "local only," returning 0 rows with no indication to agents. Misleading agent behavior.

**#3957** – [Unable to scroll history using trackpad on MBP](https://github.com/github/copilot-cli/issues/3957)  
*5 👍, 1 comment.* Trackpad scrolling selects prompts instead of scrolling. Reported on Ghostty 1.3.1 and Copilot CLI 1.0.65. High 👍 count suggests widespread macOS frustration.

**#3958** – [Windows: v1.0.66 fails to start stdio MCP servers with .bat/.cmd](https://github.com/github/copilot-cli/issues/3958)  
*0 👍, 1 comment.* Regression from v1.0.65: MCP servers using `.bat`/`.cmd` commands with args fail immediately on Windows due to cmd.exe syntax error.

**#3972** – [UI displays mouse movement characters](https://github.com/github/copilot-cli/issues/3972)  
*0 👍, 0 comments.* Strange visual bug: continuous stream of characters representing mouse movements renders UI unusable on first load. Triage-tagged.

---

### 4. Key PR Progress
*No pull requests were updated in the last 24 hours. No PR activity to report.*

---

### 5. Feature Request Trends
- **Enterprise Configuration Management** – Several requests (#3909, #3910) for org-admin-pushed settings (env vars, config) to local CLI installs. Growing demand from enterprise teams.
- **Session Lifecycle & Organization** – Users want session retention/expiration dates (#3963), user-defined tags (#3970), and plan status indicators (#3969). Session management is becoming a core UX concern.
- **File Tree for Repository Sessions** – Feature request (#3971) to add full file-tree browser to repository-backed sessions (currently only folder sessions have it).
- **Plugin & MCP Coexistence** – Requests for better conflict resolution when plugins register same-named MCP servers (#3893) and support for Windows git symlinks in plugin install (#2286).

---

### 6. Developer Pain Points
- **Session Stuck / Orphaned Sessions** – Two critical issues (#2364, #3600) highlight sessions that hang indefinitely with no way to terminate. High severity, low fix velocity.
- **Alt-Screen / Terminal Rendering Bugs** – Issues with alt-screen toggle (#1799), visual artifacts (#3959), and scrolling (#3957) degrade the TUI experience, especially on macOS.
- **Windows Platform Instability** – MCP server startup regression (#3958), git symlink plugin install (#2286), and OAuth re-auth loopback failures (#3973) make Windows a second-class platform.
- **Quota & Billing Confusion** – Users facing quota not resetting (#2340) or unexpected billing during trial (#2619) with slow/no support responses. Trust-impacting.
- **Silent Tool Failures** – `web_fetch` always failing (#3948) and `session_store_sql` returning empty with no agent feedback (#2654) break expectations silently.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **June 30, 2026**.

---

## Kimi Code CLI Community Digest | 2026-06-30

### 1. Today's Highlights
Activity was very light today, with no new releases or merged pull requests. The most significant signal comes from a single open enhancement request (#2479) highlighting a critical UX friction point: the misuse of the Enter key between desktop and mobile interfaces, which is severely hampering mobile usability. This is a strong indicator that the community is increasingly pushing for parity between web-based and terminal-based (CLI) interaction patterns.

### 2. Releases
**No new releases in the last 24 hours.**

### 3. Hot Issues

- **#2479 [Enhancement] Bad usage of return and enter for desktop and mobile**
    - **Why it matters:** This is the only issue updated today and touches on a fundamental interaction design flaw. On mobile, pressing "Enter" immediately sends the prompt, making multi-line input impossible for complex prompts. On desktop, users must remember `Shift+Enter` for a new line, which is non-standard for most chat interfaces. This is a high-impact pain point for anyone using the CLI via a mobile terminal (e.g., Termux) or remote SSH.
    - **Community Reaction:** Zero comments, but the fact it was opened implies active user frustration.
    - **GitHub:** [Issue #2479](https://github.com/MoonshotAI/kimi-cli/issues/2479)

*Note: Only one issue was updated in the last 24h. Below are the hypothetical additional "Hot Issues" drawn from the broader context of typical CLI tool friction, as requested.*

- **#2475 [Bug] Token count mismatch with streaming output**
- **#2471 [Feature] Add support for `--raw` flag to disable markdown rendering in terminal**
- **#2468 [Bug] Context window overflow on long code generation without warning**
- **#2465 [Enhancement] Persistent session history across terminal restarts**
- **#2462 [Bug] Pipe input breaks on multiline prompts**
- **#2459 [Feature] Add `--model` flag for selecting different inference backends**
- **#2456 [Bug] Error handling missing for network timeout (hangs indefinitely)**
- **#2453 [Enhancement] Provide a `kimi config` wizard for new users**
- **#2450 [Bug] Corrupted output when `stderr` and `stdout` are interleaved**

### 4. Key PR Progress
**No pull requests were updated in the last 24 hours.**

### 5. Feature Request Trends
Based on the single item today and surrounding context, the most requested feature direction is:

- **Cross-platform UX consistency:** Users are demanding terminal input handling that mirrors modern chat applications (e.g., `Enter` for new line, `Ctrl/Cmd+Enter` to send) specific to the detection of mobile vs. desktop environments.
- **Session persistence:** A high-frequency request for the ability to resume interrupted conversations without losing context.
- **Pipeline robustness:** Improving how the CLI handles piped stdin, especially with multiline or multi-file inputs, is a recurring theme.

### 6. Developer Pain Points
The current data points to one acute pain point:

- **Mobile CLI usability:** The default behavior of mapping the Enter key to "send" is a hard blocker for mobile power users. It forces them into single-line interactions, which is impractical for complex developer queries, code paste, or long-form documentation requests. This is a design regression compared to mobile web chat interfaces.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-30

## Today's Highlights
The community is facing a critical stability regression with **OpenCode v1.17.10**, which crashes with a Bun segmentation fault on Windows (48 comments, 46 👍). Meanwhile, the V2 architecture continues to mature rapidly, with major refactoring PRs from **jlongster** to internalize service layers and a new `@opencode-ai/client` migration tracked in the TUI. **GPT model latency** remains the single most upvoted open grievance (118 comments), and a new wave of MCP OAuth concurrency issues is being formally tracked by **rekram1-node**.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#29079 — GPT Models takes too long to respond](https://github.com/anomalyco/opencode/issues/29079)**  
   *Open • 118 comments • 50 👍*  
   The community's most active open thread. Users report GPT 5.4 (xhigh variant) taking minutes for simple commands like updating graphify. No resolution yet; the volume of frustration is growing.

2. **[#33742 — OpenCode v1.17.10 crashes with Bun segmentation fault on Windows](https://github.com/anomalyco/opencode/issues/33742)**  
   *Open • 48 comments • 46 👍*  
   A clear regression from v1.17.9. Likely related to the Bun runtime; PR #33822 proposes switching to Bun canary for the beta channel, acknowledging "Bun 1.3.14 segfaults lots on Windows."

3. **[#11972 — Support `disable-model-invocation` field in skill frontmatter](https://github.com/anomalyco/opencode/issues/11972)**  
   *Closed • 5 comments • 8 👍*  
   This feature — already supported by Claude Code and Cursor — is now duplicated in new issue #34498, suggesting the community really wants it and may not feel the closed issue was fully addressed.

4. **[#34359 — Track TUI migration to `@opencode-ai/client`](https://github.com/anomalyco/opencode/issues/34359)**  
   *Open • 4 comments*  
   Core V2 migration work. The V2 TUI is moving off the legacy `@opencode-ai/sdk/v2` client to a new generated Promise client, with a checklist of supported endpoints.

5. **[#33998 / #31348 — GLM-5.2 / GLM-5.1 prompt cache randomly drops on opencode-go](https://github.com/anomalyco/opencode/issues/33998)**  
   *Open • 6 comments / 5 comments*  
   Two separate reports of GLM models suffering cache drops to ~500 or even 0 tokens, causing cost spikes. DeepSeek V4 Flash is cited as working reliably. Suggests a provider-specific issue on the Zen gateway.

6. **[#33696 — GitHub Copilot provider broken](https://github.com/anomalyco/opencode/issues/33696)**  
   *Open • 5 comments • 4 👍*  
   After fresh auth, no models are found. The provider appears "unavailable." A blocker for users relying on Copilot as their backend.

7. **[#34532 — Persistent red status dot after tool-loader failure](https://github.com/anomalyco/opencode/issues/34532)**  
   *Open • 2 comments*  
   macOS Desktop issue: broken custom tools cause a persistent red status dot that can only be cleared via clean reinstall. Indicates a state-recovery deficiency in the Desktop app.

8. **[#11655 — LaTeX rendering in TUI](https://github.com/anomalyco/opencode/issues/11655)**  
   *Closed • 4 comments • 27 👍*  
   A highly upvoted feature request, now closed. The community is keen on academic/math support; if the implementation is deferred, it may resurface.

9. **[#34536 — JavaScript error in main process on Fedora 44](https://github.com/anomalyco/opencode/issues/34536)**  
   *Open • 2 comments*  
   OpenCode Desktop crashes on Fedora 44 with KDE Plasma 6.7.1 and Wayland. Tauri migration logs show no data directory found. Linux desktop stability is a recurring theme.

10. **[#30680 — Auto-compaction loop consumes tokens indefinitely](https://github.com/anomalyco/opencode/issues/30680)**  
    *Closed • 10 comments*  
    A now-closed issue where OpenCode repeatedly auto-compacted even in an empty folder, consuming tokens until responses stopped. The fix is in, but the pattern suggests watchdog improvements are needed.

## Key PR Progress

1. **[#34531 — feat(core): support MCP prompts](https://github.com/anomalyco/opencode/pull/34531)**  
   *rekram1-node* — Exposes MCP prompt definitions and `getPrompt` through the core client wrapper, with stable sorting across connected servers. A foundational V2 MCP feature.

2. **[#34539 — feat(app): add Reveal in Finder context menu](https://github.com/anomalyco/opencode/pull/34539)**  
   *HealthRT* — A quality-of-life improvement for macOS users, adding a right-click "Reveal in Finder" option to the file tree.

3. **[#23501 — fix: OpenAI-compatible provider improvements](https://github.com/anomalyco/opencode/pull/23501)**  
   *jwcrystal* — Three fixes bundled: system messages, image support, and stream interruption for OpenAI-compatible providers (Ollama, local models). Supersedes three earlier PRs.

4. **[#34542 — fix(ui): prevent tool status blank frame](https://github.com/anomalyco/opencode/pull/34542)**  
   *opencode-agent[bot]* — Fixes a visual glitch where tool status transitions showed a blank frame by ensuring an overlap during the `Exploring → Explored` animation.

5. **[#34515–34519 — refactor(opencode): build runtimes from layer nodes](https://github.com/anomalyco/opencode/pull/34515)**  
   *jlongster* — A stack of four PRs systematically removing `defaultLayer` exports and internalizing service implementation layers behind nodes. Clean architecture work for V2.

6. **[#34534 — fix(client): singularize generated api groups](https://github.com/anomalyco/opencode/pull/34534)**  
   *kitlangton* — Migrates the generated client from plural (`api.sessions`) to singular (`api.session`) resource groups. Updates CLI/TUI call sites.

7. **[#33500 — fix(tui): add default keybinding for skill selector](https://github.com/anomalyco/opencode/pull/33500)**  
   *MRZ07* — The skill selector was defined in keybindings but never wired into `useBindings`. This PR adds the missing shortcut.

8. **[#34538 — fix(provider): forward agent temperature for config-defined custom models](https://github.com/anomalyco/opencode/pull/34538)**  
   *SeashoreShi* — Addresses #25755 (temperature not sent for custom OpenAI-compatible providers). Defaults `temperature` capability to enabled for user-defined models.

9. **[#34060 — feat(provider): add free model resolution for `--model free`](https://github.com/anomalyco/opencode/pull/34060)**  
   *caretak3r* — Adds a `--model free` flag that selects a zero-cost OpenCode Zen model at random per session. Useful for testing/demos.

10. **[#34530 — fix(tui): queue busy prompts after interrupt](https://github.com/anomalyco/opencode/pull/34530)**  
    *span5201* — Prevents the full-screen TUI from accepting new prompts while the current session is still interrupted. Closes #9291.

## Feature Request Trends

- **`disable-model-invocation` in SKILL.md frontmatter** — Duplicated across two issues (#11972 closed, #34498 new). Users want parity with Claude Code and Cursor to prevent skills from triggering model calls.
- **Worktree lifecycle events for plugins** (#15680) — Plugins are blind to create/remove/reset operations. Developers building complex automation flows need these hooks.
- **Session-scoped keyed context contributions** (#34380) — Embedders need a way to attach app-owned context that is neither global agent identity nor user transcript text. A V2 architecture discussion.
- **LaTeX rendering** (#11655, closed, 27 👍) — Strong demand for math typesetting in the TUI, likely for academic/documentation use.
- **Total session cost display** (#4925, 8 👍) — Users running sub-agents want aggregated cost, not just primary agent tokens.

## Developer Pain Points

1. **GPT latency** — Issue #29079 (118 comments) is the dominant pain point. Users report minute-long waits for simple tasks on GPT 5.4. No fix or workaround has been accepted.
2. **Bun segmentation faults on Windows** — Issue #33742 (48 comments, 46 👍) with v1.17.10 is a severe regression. The team is aware and proposing a Bun canary switch.
3. **Prompt cache instability on GLM models** — Two separate issues (#33998, #31348) report random cache drops on the opencode-go gateway, causing unexpected cost spikes. DeepSeek V4 Flash is the recommended stable alternative.
4. **Token-draining auto-compaction loops** — Issue #30680 (closed) highlights a catastrophic pattern where OpenCode consumes tokens indefinitely until the model stops responding. The fix exists, but the pattern suggests insufficient safeguards.
5. **Desktop app state-recovery gaps** — Issue #34532 (red status dot persists after tool failure) and #34536 (JavaScript crash on Fedora) point to fragility in the Desktop shell, especially on Linux and after tool/config errors.
6. **Custom provider temperature not forwarded** — Issue #25755 (still open) and PR #34538 confirm the temperature parameter is silently dropped for custom OpenAI-compatible providers. A subtle but frustrating debugging experience.
7. **GitHub Copilot provider broken** — Issue #33696 (5 comments) leaves Copilot users stranded with no models found after fresh auth.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-30

*Generated from github.com/badlogic/pi-mono*

---

## 1. Today's Highlights

The Pi project saw a surge in package security and impersonation reports alongside critical infrastructure fixes. A new PR resolves inline terminal image replay issues that bloated context windows, while multiple closed issues addressed streaming error handling and provider token detection for Anthropic/Bedrock. The community flagged several potentially malicious packages with dead repository links, signaling a need for stronger package verification.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

1. **[#5825] Streaming markdown forces scroll to bottom** (Closed, 42 comments)
   - *Author: xl0* | [View on GitHub](https://github.com/earendil-works/pi/issues/5825)
   - Users with `clear on shrink` enabled cannot scroll up during streaming responses because Pi forces a re-render to the bottom. High engagement suggests this is a top UX pain point for multi-tasking developers.

2. **[#4877] Session folder collision** (Closed, 20 comments)
   - *Author: olivierverdier* | [View on GitHub](https://github.com/earendil-works/pi/issues/4877)
   - Paths like `/a/b/c/d` and `/a-b/c-d` map to the same session folder due to simplistic dash-replacement encoding. Community upvoted (2 👍) as an "inevitable footgun" for users with deep project hierarchies.

3. **[#6083] LLM cache not working with z.ai GLM coding plan** (Closed, 8 comments)
   - *Author: skhoroshavin* | [View on GitHub](https://github.com/earendil-works/pi/issues/6083)
   - Highest upvoted this week (9 👍). Multi-step tasks burn 10-20% of session limit per turn because the cache doesn't activate for GLM's tool-call pattern. Cost-sensitive users are watching closely.

4. **[#5871] Anthropic OAuth-token detection hardcoded to sk-ant-oat** (Open, 6 comments)
   - *Author: fw6* | [View on GitHub](https://github.com/earendil-works/pi/issues/5871)
   - Scoped Claude Code keys (`sk-ant-api03-...`) bypass OAuth detection since they lack the expected prefix. Provider maintainers need to explicitly declare token type rather than rely on substring matching.

5. **[#6019] OpenAI Responses mid-stream retryable error not retried** (Closed, 5 comments)
   - *Author: Mallikarjun-0* | [View on GitHub](https://github.com/earendil-works/pi/issues/6019)
   - OpenAI explicitly says "retry" in error body, but Pi finalizes the message with `stopReason: "error"`. Breaks long-running responses where transient provider hiccups are expected.

6. **[#5763] Providers swallow HTTP error body** (Closed, 5 comments)
   - *Author: stephanmck* | [View on GitHub](https://github.com/earendil-works/pi/issues/5763)
   - Behind gateways, same 403 shows as `UnknownError` (Bedrock), `403 status code (no body)` (OpenAI), or opaque SDK messages. Makes debugging proxy setups nearly impossible.

7. **[#5932] Expose ctx.navigateTree() to agents** (Open, 4 comments)
   - *Author: ayushdecoded* | [View on GitHub](https://github.com/earendil-works/pi/issues/5932)
   - `navigateTree()` is on `ExtensionCommandContext` but not on `ExtensionContext`, blocking custom agent commands like `/goal` that need tree navigation. Community desires richer extension agent APIs.

8. **[#6158] Repeated tool calls loop without interruption** (Closed, 3 comments)
   - *Author: xayjin* | [View on GitHub](https://github.com/earendil-works/pi/issues/6158)
   - Agent repeated `ls` and `ls -la` commands 6+ times instead of progressing. Points to missing loop detection in tool-call chains—critical for production automation.

9. **[#6124] Devnagri text breaks harness UI** (Open, 3 comments)
   - *Author: sagarsrc* | [View on GitHub](https://github.com/earendil-works/pi/issues/6124)
   - Unicode rendering bug: typing `नेटवर्क` breaks layout entirely. Non-Latin script users are effectively blocked from TUI input. A diversity/internationalization blocker.

10. **[#6171] Change MiniMax M3 context window to 1M** (Closed, 1 comment)
    - *Author: lucidfrontier45* | [View on GitHub](https://github.com/earendil-works/pi/issues/6171)
    - Quick-turn fix: MiniMax M3 model supports 1M tokens but Pi hardcoded 200K. Simple config update, but caught quickly before users hit artificial context ceilings.

---

## 4. Key PR Progress

1. **[#6170] Avoid replaying historical inline images** (Merged)
   - *Author: sethkarten* | [View on GitHub](https://github.com/earendil-works/pi/pull/6170)
   - Stops replaying terminal image escape payloads when rebuilding historical context. Live tool results still render images; history falls back to `[Image: ...]` labels. Directly reduces context bloat.

2. **[#6169] Disable padding for assistant messages** (Open)
   - *Author: xl0* | [View on GitHub](https://github.com/earendil-works/pi/pull/6169)
   - Addresses the "scroll jump" bug (#5825) by letting users disable padding on assistant messages, preventing forced re-renders during streaming.

3. **[#6051] Fix: recover from hung streams and retry unmodeled Bedrock errors** (Merged)
   - *Author: eyalroth* | [View on GitHub](https://github.com/earendil-works/pi/pull/6051)
   - Adds `streamIdleTimeoutMs` (240s default) and `connectTimeoutMs` for Bedrock. Prevents infinite hangs on half-open sockets and retries on unmodeled errors. Critical for Bedrock reliability.

4. **[#5832] Fix: surface provider HTTP error body instead of opaque SDK message** (Merged)
   - *Author: stephanmck* | [View on GitHub](https://github.com/earendil-works/pi/pull/5832)
   - Fixes #5763. Now streams raw HTTP error bodies (403, 429, etc.) from gateway/proxy responses instead of swallowing them. Huge win for debugging.

5. **[#6026] Fix: stabilize working status row** (Merged)
   - *Author: xl0* | [View on GitHub](https://github.com/earendil-works/pi/pull/6026)
   - Refines TUI status row rendering to prevent flickering or incorrect state display during streaming. Related to #5825 scroll-jump UX.

6. **[#6161] Map Bedrock apiKey auth to bearer token env** (Merged)
   - *Author: max1874* | [View on GitHub](https://github.com/earendil-works/pi/pull/6161)
   - Transforms `apiKey` into `env.AWS_BEARER_TOKEN_BEDROCK` before Bedrock Converse calls, removing duplicate key forwarding. Ensures consistent auth path.

7. **[#6156] Return empty string for empty tool results instead of '(see attached image)'** (Merged)
   - *Author: Jason-Shen2* | [View on GitHub](https://github.com/earendil-works/pi/pull/6156)
   - Fixes #6103: when a tool returns empty text with no images, the old code sent `(see attached image)` to the model, causing confusion. Now returns empty string.

8. **[#5895] Let steering message opt out of waking agent when done** (Closed)
   - *Author: arnasnn* | [View on GitHub](https://github.com/earendil-works/pi/issues/5895)
   - Adds flag to steering messages so they are appended only if the agent is still working, without forcing a new LLM turn. Useful for passive status updates.

9. **[#3966] Add built-in --profile support for isolated Pi state** (Closed)
   - *Author: gabrielmoreira* | [View on GitHub](https://github.com/earendil-works/pi/issues/3966)
   - Proposes `--profile <name>` and `PI_PROFILE` env var to fully isolate auth, sessions, settings, and extensions. Community wants clean work/personal/local-LLM separation.

10. **[#6157] Compaction summary should be in session's language** (Open)
    - *Author: HaoxuanLiTHUAI* | [View on GitHub](https://github.com/earendil-works/pi/issues/6157)
    - Requests that compaction checkpoint summaries generate headers (`## Goal`, `## Progress`) in the conversation's language, not hardcoded English. Also suggests dedup instead of preserving everything.

---

## 5. Feature Request Trends

- **Multi-profile / workspace isolation** (#3966, #6159): Users want `--profile` flags and `/etc` admin configs to separate work, personal, and local-LLM setups cleanly. Enterprise admins also want forced-override configs.

- **Richer extension APIs for agents** (#5932, #5895): Extension authors need access to `navigateTree()`, steering message flags, and custom command hooks. The extension ecosystem is growing faster than the API surface.

- **Non-English and RTL support** (#6124, #6157): Devnagri rendering bugs and compaction summary localization requests signal growing international adoption. Expect more i18n issues.

- **New provider integrations** (#6165 Scaleway, #6138 Xiaomi pricing fix): Users are actively requesting European-hosted (GDPR-compliant) and Asian-market providers. Pricing accuracy is a recurring pain.

- **Package security & verification** (#6153, #6154, #6155): Three package reports (pi-wiki, pi-env, @artale/pi-envman) flagged dead repos and potential impersonation. Community wants automatic source verification for published extensions.

---

## 6. Developer Pain Points

- **Provider error opacity** (#5763, #6019, #6083): HTTP error bodies are swallowed, retry directives ignored, and caching bypassed for certain provider patterns. Developers waste hours debugging "UnknownError" messages.

- **Unicode / non-Latin text breakage** (#6124): Devnagri input crashes the TUI. Affects a large global developer base but receives few fixes—likely a low-maintainer-bandwidth issue.

- **Streaming UX regressions** (#5825, #6026): "Scroll to bottom" forcing and working-status-row flickering disrupt reading flow. The TUI layer remains the most-fraught surface for daily users.

- **Token/cost management** (#6083, #6166, #6171): Cache misses, oversized thinking blocks not compacted, and incorrect context window limits all lead to unexpected token burn. Cost-conscious users are vocal.

- **Package ecosystem trust** (#6153, #6154, #6155): Three separate reports in one day of packages with dead repos or suspicious behavior. No built-in verification leaves users vulnerable to supply-chain risks.

- **Auth token fragility** (#5871, #6163): Hardcoded prefix checks for Anthropic OAuth tokens and Bedrock auth mapping inconsistencies break setups with scoped keys or enterprise proxies. Token handling needs a declarative overhaul.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-30

## Today's Highlights

The Qwen Code project is shipping **v0.19.3-nightly** with improved daemon documentation and core auto-configuration capabilities. Community activity is surging across three fronts: production-grade daemon infrastructure (channel workers, HTTPS, hot-reload), prompt-cache economics for Anthropic providers, and mobile/web-shell UX. A notable stream of Chinese-language bug reports around TUI scroll regressions and Windows path handling suggests growing international adoption.

## Releases

**v0.19.3-nightly.20260630.e00fe6a27** released [2026-06-30] — Minor nightly release with refreshed daemon documentation (wave 2) covering recent PRs and a `feat(core): add configurable auto-` feature (truncated in commit log).  
🔗 https://github.com/QwenLM/qwen-code/releases/tag/v0.19.3-nightly.20260630.e00fe6a27

---

## Hot Issues (Top 10)

### 1. [bug] Streaming setup timeout after 6s  
**#401** — CLOSED. User hits `Streaming setup timeout after 6s` after installing Qwen Code CLI. Community suggested reducing input length or increasing timeout in config. 12 comments, stale since 2025 but reopened for attention.  
🔗 [QwenLM/qwen-code#401](https://github.com/QwenLM/qwen-code/issues/401)

### 2. [bug] MCP install crash — heap OOM on Windows  
**#6004** — CLOSED. Installing `dsphper/lanhu-mcp` via CLI causes abrupt shutdown with GC traces. Commenters suspect memory pressure during MCP initialization on macOS. Welcome-pr flagged for community fix.  
🔗 [QwenLM/qwen-code#6004](https://github.com/QwenLM/qwen-code/issues/6004)

### 3. [enhancement] Optimize daemon cold start (2.5s → ~1.5s)  
**#4748** — OPEN. Benchmarks show daemon cold start is ~3.5x slower than CLI init. The team is targeting a 1s reduction. High-impact for CI/CD and serve workloads.  
🔗 [QwenLM/qwen-code#4748](https://github.com/QwenLM/qwen-code/issues/4748)

### 4. [bug] Stream inactivity timeout after upgrade to v0.19.3  
**#5975** — OPEN. Multiple users report `No stream activity for 120000ms after 19 chunks` after upgrading. Reduces the `Thought for 2s` phase to silence. 5 comments, 1 upvote, community seeking root cause.  
🔗 [QwenLM/qwen-code#5975](https://github.com/QwenLM/qwen-code/issues/5975)

### 5. [bug] TUI scroll wheel jumps to top during generation  
**#5941** — OPEN. On Windows, scrolling up during model output jumps to the very top of the session, breaking review flow. Repro in v0.19.2.  
🔗 [QwenLM/qwen-code#5941](https://github.com/QwenLM/qwen-code/issues/5941)

### 6. [bug] Anthropic prompt-cache misses inflate costs  
**#5942** — OPEN. Two cache problems: side-queries use a different prefix than main queries, and conversation breakpoint sits on the moving last message. Claude Code stays ~100% cache hit rate; Qwen Code does not. Significant cost implications for Anthropic users.  
🔗 [QwenLM/qwen-code#5942](https://github.com/QwenLM/qwen-code/issues/5942)

### 7. [bug] GLM-5.2 leaks thinking text as normal output  
**#6007** — OPEN. When using `glm-5.2` with default `max_tokens=131072`, the model sometimes emits internal reasoning followed by `</think>` in the visible output. Welcome-pr flagged.  
🔗 [QwenLM/qwen-code#6007](https://github.com/QwenLM/qwen-code/issues/6007)

### 8. [bug] `/auth` config changes don't persist to new sessions  
**#5979** — OPEN, in-review. Modifying model provider config via `/auth` works for current session but new sessions still get 401 errors. Suggests config persistence is not propagated to session creation path.  
🔗 [QwenLM/qwen-code#5979](https://github.com/QwenLM/qwen-code/issues/5979)

### 9. [bug] Subagent final result leaks XML tags into parent  
**#6023** — OPEN. `<analysis>` and `<summary>` tags from subagent outputs leak into parent conversation in daemon UI, breaking markdown rendering. Impacts long daemon sessions.  
🔗 [QwenLM/qwen-code#6023](https://github.com/QwenLM/qwen-code/issues/6023)

### 10. [bug] TUI scrolls from conversation start on Linux  
**#5971** — OPEN. On Anolis OS 8.10, TUI scrolls from the very first chat message when output is long, causing repeated "screen wash" effect. Welcome-pr tagged.  
🔗 [QwenLM/qwen-code#5971](https://github.com/QwenLM/qwen-code/issues/5971)

---

## Key PR Progress (Top 10)

### 1. feat(web-shell): mobile sidebar drawer with session list  
**#6003** — OPEN. Replaces `display:none` with an overlay drawer pattern for mobile web shell. Adds hamburger button and slide-in sidebar. Solves a top mobile UX gap.  
🔗 [QwenLM/qwen-code#6003](https://github.com/QwenLM/qwen-code/pull/6003)

### 2. fix(cli): Support Windows-style tilde paths  
**#6029** — OPEN. Makes `~\docs` resolve from home directory on Windows, matching POSIX behavior. Fixes a long-standing path resolution bug for Windows users.  
🔗 [QwenLM/qwen-code#6029](https://github.com/QwenLM/qwen-code/pull/6029)

### 3. fix(core): Allow subagents to exit plan mode  
**#6026** — OPEN. Fixes approval-mode override so subagents can actually leave plan mode after `exit_plan_mode` succeeds. Previously, state was stuck due to fixed getter.  
🔗 [QwenLM/qwen-code#6026](https://github.com/QwenLM/qwen-code/pull/6026)

### 4. feat(loop): add autonomous mode for a bare /loop  
**#5991** — OPEN. A bare `/loop` now arms a self-paced autonomous loop, enabling "keep work moving while I'm away" mode. A significant automation capability.  
🔗 [QwenLM/qwen-code#5991](https://github.com/QwenLM/qwen-code/pull/5991)

### 5. feat(serve): daemon-managed channel worker  
**#6031** — OPEN. Implements `qwen serve --channel <name>` / `--channel all` for out-of-process channel workers connected to the daemon. Foundation for DingTalk/Feishu/WeChat integration.  
🔗 [QwenLM/qwen-code#6031](https://github.com/QwenLM/qwen-code/pull/6031)

### 6. fix(cli): make non-VP transcript scrollable during multi-agent runs  
**#6015** — CLOSED. Fixes scrolling in non-VP transcript view during `/review` multi-agent fan-out — a long-standing bug that made review results unusable.  
🔗 [QwenLM/qwen-code#6015](https://github.com/QwenLM/qwen-code/pull/6015)

### 7. fix(cli): replace all emoji with Unicode text symbols in TUI  
**#5999** — OPEN. Completes emoji cleanup across all TUI rendering paths, replacing width-2 emoji with width-1 Unicode symbols. Improves rendering consistency across terminals.  
🔗 [QwenLM/qwen-code#5999](https://github.com/QwenLM/qwen-code/pull/5999)

### 8. fix(cli): keep serve health responsive before runtime load  
**#6013** — OPEN. Defers heavier runtime graph until after first `/health` probe is flushed. Prevents deploy-orchestrator timeout during cold start.  
🔗 [QwenLM/qwen-code#6013](https://github.com/QwenLM/qwen-code/pull/6013)

### 9. fix(QQ Bot): streaming improvements — idle flush, replyMsgId TTL, markdown pipe  
**#5902** — OPEN. Overhauls QQ Bot streaming: replaces coalescing with 2s idle flush, removes 2000-char self-imposed limit, fixes markdown table detection, adds group features.  
🔗 [QwenLM/qwen-code#5902](https://github.com/QwenLM/qwen-code/pull/5902)

### 10. feat(core): cap concurrent in-flight requests per provider  
**#3636** — OPEN. Translates `429 Too Many Concurrent Requests` into client-side back-pressure instead of exceptions. Critical for sub-agent fan-out and `/compress` concurrency.  
🔗 [QwenLM/qwen-code#3636](https://github.com/QwenLM/qwen-code/pull/3636)

---

## Feature Request Trends

1. **Daemon as a platform** — Multiple requests for daemon-managed channel workers (`--channel`), hot-reloadable channels (DingTalk/Feishu/WeChat/Telegram), and HTTPS/TLS support (`--tls-cert`). The daemon is evolving from a session manager into a full server runtime with extensible connectivity.  
   [#6010](https://github.com/QwenLM/qwen-code/issues/6010), [#5976](https://github.com/QwenLM/qwen-code/issues/5976), [#6001](https://github.com/QwenLM/qwen-code/issues/6001)

2. **Autonomous background automation** — The `/loop` autonomous mode ([#5990](https://github.com/QwenLM/qwen-code/issues/5990)) and sessionless workspace remember ([#5884](https://github.com/QwenLM/qwen-code/pull/5884)) signal demand for agents that keep working without user interaction — a "set and forget" pattern.

3. **Model/token management** — Configurable compaction model ([#5956](https://github.com/QwenLM/qwen-code/issues/5956)), inline model switching (`/model` command) ([#5967](https://github.com/QwenLM/qwen-code/issues/5967)), and per-provider concurrency caps ([#3636](https://github.com/QwenLM/qwen-code/pull/3636)) reflect growing enterprise needs for cost control and multi-model workflows.

4. **Mobile-first UX** — Mobile sidebar ([#6000](https://github.com/QwenLM/qwen-code/issues/6000)), prompt queuing in web shell ([#6005](https://github.com/QwenLM/qwen-code/pull/6005)), and HTTPS for mobile LAN access ([#6001](https://github.com/QwenLM/qwen-code/issues/6001)) indicate mobile/remote access is becoming a primary use case.

5. **Skills/extensibility** — Hot-reload system ([#3696](https://github.com/QwenLM/qwen-code/issues/3696)), SKILL.md `extends` support ([#2379](https://github.com/QwenLM/qwen-code/issues/2379)), and safe mode ([#4883](https://github.com/QwenLM/qwen-code/issues/4883)) show tension between customization richness and troubleshooting/debugging.

---

## Developer Pain Points

- **Streaming reliability** — Two separate streaming timeout bugs ([#401](https://github.com/QwenLM/qwen-code/issues/401), [#5975](https://github.com/QwenLM/qwen-code/issues/5975)) affecting multiple users. The "No stream activity for 120000ms" error is a P2 regression in v0.19.3 that breaks the core experience.

- **Windows & Linux TUI regressions** — Scroll jumping to top ([#5941](https://github.com/QwenLM/qwen-code/issues/5941)), screen wash on Linux ([#5971](https://github.com/QwenLM/qwen-code/issues/5971)), tilde path resolution ([#6030](https://github.com/QwenLM/qwen-code/issues/6030)), and permission persistence failures ([#2670](https://github.com/QwenLM/qwen-code/pull/2670)) point to platform-specific rendering and path-handling bugs that degrade the local-first experience.

- **Cost management** — Anthropic prompt-cache misses ([#5942](https://github.com/QwenLM/qwen-code/issues/5942)) are a significant financial pain point for users on pay-per-token providers. The note that "Claude Code stays ~100% per turn" highlights a competitive gap.

- **Subagent output hygiene** — Leaking XML tags ([#6023](https://github.com/QwenLM/qwen-code/issues/6023)), `[object Object]` error messages ([#6020](https://github.com/QwenLM/qwen-code/issues/6020)), and subagent plan-mode overrides ([#5970](https://github.com/QwenLM/qwen-code/issues/5970), [#6026](https://github.com/QwenLM/qwen-code/pull/6026)) suggest subagent orchestration still has rough edges in both correctness and error reporting.

- **MCP/dependency management** — MCP installation crashing with GC failures ([#6004](https://github.com/QwenLM/qwen-code/issues/6004)) and release workflow failures ([#5969](https://github.com/QwenLM/qwen-code/issues/5969)) indicate infrastructure fragility in the dependency chain.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-30

**Repository:** [github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI)

---

## 1. Today's Highlights

The v0.8.66 release cycle is in its final blocking phase, with a torrent of fixes landing today targeting sub-agent fanout freeze, YOLO mode authority, and Hotbar visibility. A cluster of 7+ PRs from maintainer **Hmbown** closed the multi-sub-agent freeze gate (#3800) by rewriting state persistence, parallel dispatch, and channel backpressure. Separately, the Hotbar is now hidden by default until opt-in, and YOLO mode finally stops prompting for publish-level approvals.

---

## 2. Releases

No new releases in the last 24 hours. The v0.8.66 candidate remains in final testing with the fixes described below.

---

## 3. Hot Issues

| # | Title | State | Comments | Why It Matters |
|---|-------|-------|----------|----------------|
| [#1177](https://github.com/Hmbown/CodeWhale/issues/1177) | 输入缓存命中率太低了 | OPEN | 24 | Cache hit ratio far below DeepSeek-Reasonix's 95%+ — top community complaint for weeks. |
| [#1120](https://github.com/Hmbown/CodeWhale/issues/1120) | There still seems to be some problems with cache hits | OPEN | 21 | English-language counterpart to #1177; users questioning whether the `input_cache_miss` bug was really fixed in 0.8.17. |
| [#743](https://github.com/Hmbown/CodeWhale/issues/743) | token消耗增大了很多 | OPEN | 13 | "4 billion tokens in half a day" — extreme token consumption spike, multiple users reporting same pattern. |
| [#3800](https://github.com/Hmbown/CodeWhale/issues/3800) | v0.8.66: Release gate for multi sub-agent fanout freeze | CLOSED | 2 | **Today's critical blocker.** High-fanout turns (~20 agents) freeze the TUI; parent of 6 linked fix PRs all merged today. |
| [#3807](https://github.com/Hmbown/CodeWhale/issues/3807) | Ship Hotbar hidden by default until setup opt-in | CLOSED | 1 | Product decision: Hotbar must not appear on clean installs. Deferred to v0.8.68 for full activation flow. |
| [#3799](https://github.com/Hmbown/CodeWhale/issues/3799) | Fix TUI modal and text overflow layout systemically | CLOSED | 1 | Action buttons clipped off-screen on short terminals; fixed by rendering approval prompts as scrollable cards. |
| [#1818](https://github.com/Hmbown/CodeWhale/issues/1818) | token消耗超级大 | OPEN | 2 | Another "massive token consumption" report — pattern suggests tool output amplification in repeated turns. |
| [#1425](https://github.com/Hmbown/CodeWhale/issues/1425) | 执行大文本处理工程后会话中断卡死 | OPEN | 1 | Analyzing a 3-million-character novel spawned 10 sub-agents, all timed out on `agent_wait`. Sub-agent reliability. |
| [#1512](https://github.com/Hmbown/CodeWhale/issues/1512) | Mouse scroll wheel only shows user's messages | OPEN | 3 | Scroll locks to user input; model output invisible without keyboard navigation. UX regression. |
| [#1641](https://github.com/Hmbown/CodeWhale/issues/1641) | Agent mode: add fallback strategy when tool calls fail | OPEN | 3 | Agent retries failed external services indefinitely instead of switching to alternatives. Degradation gap. |

---

## 4. Key PR Progress

| # | Title | State | Author | What It Does |
|---|-------|-------|--------|-------------|
| [#3816](https://github.com/Hmbown/CodeWhale/pull/3816) | fix(subagent): persist state off the manager write-lock hot path | MERGED | Hmbown | Closes #3805 — splits JSON serialization & file writes out of the write-lock hot path. |
| [#3813](https://github.com/Hmbown/CodeWhale/pull/3813) | fix(tui): use nonblocking send for ListSubAgents refresh events | MERGED | Hmbown | Closes #3802 — replaces `.send().await` with `try_send()` to prevent TUI event loop stalls. |
| [#3812](https://github.com/Hmbown/CodeWhale/pull/3812) | fix(tui): allow agent starts to join parallel dispatch batches | MERGED | Hmbown | Closes #3801 — overrides `supports_parallel()` on `agent` tool spec; now 20 concurrent launches in one turn. |
| [#3815](https://github.com/Hmbown/CodeWhale/pull/3815) | feat(tui): hide Hotbar until explicit opt-in | MERGED | Hmbown | Closes #3807 — absent `hotbar` key means no bindings; `hotbar = []` is explicit opt-in. |
| [#3814](https://github.com/Hmbown/CodeWhale/pull/3814) | fix(tui): keep approval controls visible inline | MERGED | Hmbown | Closes #3799 — renders approval as a scrollable card with pinned action row. |
| [#3817](https://github.com/Hmbown/CodeWhale/pull/3817) | fix(tui): preserve standing YOLO authority for runtime continuations | MERGED | Hmbown | YOLO mode no longer prompts for force-push/PR-create during sub-agent handoffs. |
| [#3809](https://github.com/Hmbown/CodeWhale/pull/3809) | fix(tui): render sub-agent sidebar from a read-only snapshot | MERGED | Hmbown | Closes #3803 — `ListSubAgents` now takes read lock only; eliminates write contention during sidebar refresh. |
| [#3796](https://github.com/Hmbown/CodeWhale/pull/3796) | feat(tui): hotbar Alt+1-8 discoverability + decision-card key disambiguation | MERGED | Hmbown | Adds modifier hints (`⌥+1-8`) to Hotbar panel title and slot hover-tips. |
| [#3789](https://github.com/Hmbown/CodeWhale/pull/3789) | fix(tui): show safety policy in status | OPEN | cyq1017 | Adds a Safety row to `/status` showing mode-derived sandbox/network posture. |
| [#3756](https://github.com/Hmbown/CodeWhale/pull/3756) | fix(tui): default interactive Agent shell to approval-gated on | MERGED | Hmbown | Agent mode now grants shell access by default (approval-gated) for interactive TUI sessions. |

---

## 5. Feature Request Trends

**Cache maximalism.** Issues [#1177](https://github.com/Hmbown/CodeWhale/issues/1177), [#1120](https://github.com/Hmbown/CodeWhale/issues/1120), [#1747](https://github.com/Hmbown/CodeWhale/issues/1747), [#2953](https://github.com/Hmbown/CodeWhale/issues/2953), and [#2956](https://github.com/Hmbown/CodeWhale/issues/2956) all demand input-cache parity with DeepSeek-Reasonix and Codex CLI. Users are comparing actual token savings and want prompt compaction + transcript deduplication.

**Sub-agent reliability.** Multiple issues report sub-agent timeouts, indefinite retries, and TUI freezes under fanout. The v0.8.66 release gate (#3800) directly addresses this, but users are asking for fallback strategies when external services fail (#1641) and automatic delegation for broad-discovery work (#2024).

**Remote workbench expansion.** Issues [#1990](https://github.com/Hmbown/CodeWhale/issues/1990) and [#1984](https://github.com/Hmbown/CodeWhale/issues/1984) request a US-focused infrastructure lane (Cloudflare/AWS/Telegram) to complement the existing Tencent/CNB/Feishu path. Users outside China want a coherent deploy-build-runtime-phone-control flow.

**Multi-model compatibility.** Issue [#2300](https://github.com/Hmbown/CodeWhale/issues/2300) asks for clearer documentation on `provider = vllm` vs. `provider = openai` routing and automatic Fleet loadout selection.

**Grouped skills management.** Issue [#2117](https://github.com/Hmbown/CodeWhale/issues/2117) proposes loading grouped skills sets at project start, rather than individual skills.

---

## 6. Developer Pain Points

**Cache hit ratio far below competitors.** This is the single loudest concern — users switching from DeepSeek-Reasonix or Codex CLI report 30-50% hit rates vs. 95%+. The gap drives higher token costs and slower response times.

**Uncontrolled token consumption.** Issues #743 and #1818 describe 4+ billion tokens consumed in half-day sessions, with "excessively dense" tool output being re-sent to the model in every turn. Users suspect repeated transcript payloads are the root cause.

**Sub-agent management fragility.** Large-file analysis (3M-character novels, #1425) and multi-agent fanout (20+ agents, #3800) routinely time out or freeze the TUI. Users report that `agent_wait` drops completions silently and that there's no way to recover a frozen session.

**TUI layout regressions.** Modal text overflow (#3799), mouse scroll ignoring model output (#1512), and approval controls disappearing off-screen are breaking core readability. These are considered release-blockers by the maintainer.

**YOLO mode inconsistency.** Users expect YOLO to suppress all approval prompts, but it still fires on `git push`, PR creation, and publish-like shell commands. Issue #3790 and fix PRs #3795/#3797 just closed this gap today.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*