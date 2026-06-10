# AI CLI Tools Community Digest 2026-06-10

> Generated: 2026-06-10 02:03 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report
**Date:** 2026-06-10

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape shows a mature ecosystem with distinct tiers of maturity and community scale. Claude Code, OpenAI Codex, and GitHub Copilot CLI form the top tier with the highest community engagement and enterprise adoption, all facing scaling pains from safety systems, model rollouts, and session reliability. The middle tier—Gemini CLI, OpenCode, Pi, and Qwen Code—are rapidly iterating with ambitious feature work in multi-agent orchestration, MCP integration, and cross-session persistence, often directly porting innovations from Claude Code. The emerging tier (Kimi Code CLI, DeepSeek's CodeWhale) shows focused execution on specific pain points like token efficiency and hook observability. A dominant pattern is the "Claude Code diffusion effect," where features like Dynamic Workflows, MCP tooling, and persistent memory are being replicated across tools within weeks of their introduction.

---

## 2. Activity Comparison

| Tool | Open Issues (Hot/Active) | PRs Today | Release Status | Community Signal (Top Issue) |
|---|---|---|---|---|
| **Claude Code** | 10 hot issues (P0 data loss + safety regressions) | 10 PRs | v2.1.170 (today) — Fable 5 model | Safety false positives (#66728, P0) |
| **OpenAI Codex** | 10 hot issues (gpt-5.5 404 + chat history loss) | 10 PRs | rust-v0.139.0 (today) | gpt-5.5 rollout failure (#26892, 79 comments) |
| **Gemini CLI** | 10 hot issues (agent hangs + subagent reporting) | 10 PRs | v0.47.0-preview.0 (today) | Agent hang (#21409, P1) |
| **GitHub Copilot CLI** | 10 hot issues (CLI parity + model inconsistency) | 1 PR (low quality) | v1.0.61 (yesterday) | CLI command parity (#53, 75👍) |
| **OpenCode** | 10 hot issues (memory leaks + sandboxing) | 10 PRs | No release today | Memory megathread (#20695, 64👍) |
| **Pi** | 10 hot issues (trust UX + thinking bugs) | 10 PRs | v0.79.1 (today) | Project trust (#5514, 24 comments) |
| **Qwen Code** | 10 hot issues (MCP security + daemon gaps) | 10 PRs | v0.18.0-preview.0/1 (today) | Daemon capability (#4514, 14 comments) |
| **Kimi Code CLI** | 2 hot issues (edit tool failures + loops) | 1 PR | No release today | Infinite file loop (#640, 5+ months open) |
| **DeepSeek CodeWhale** | 10 hot issues (spontaneous actions + rebrand friction) | 10 PRs | v0.8.55 (today) | Unrequested actions (#2942) |

**Key observations:**
- **Claude Code** has the highest combined signal (P0 data loss *and* safety regressions during a major model launch)
- **OpenAI Codex** and **Gemini CLI** show steady PR throughput (10 each), but Codex's gpt-5.5 failure is the highest-comment issue across all tools today
- **Copilot CLI** is unusually quiet on PRs (1 low-quality) despite high issue engagement
- **Kimi Code CLI** has the lowest activity, with only 2 hot issues and 1 PR
- **Pi** and **Qwen Code** show the fastest feature iteration velocity, each landing 10+ PRs

---

## 3. Shared Feature Directions

### A. Multi-Agent Orchestration & Workflow Systems
- **Claude Code**: Dynamic Workflows (JS sandbox + `agent()` calls)
- **OpenAI Codex**: MultiAgentV2, agent identity, HAI single-run-task (#19047-19051)
- **Gemini CLI**: Agent Teams, parallel sub-agent coordination (#4844)
- **Qwen Code**: Agent Team mode with parallel sub-agents (#4844)
- **CodeWhale**: Sub-agent session management (#2656)
- **Common need**: Better error reporting when sub-agents fail silently, configurable delegation behavior

### B. MCP Ecosystem Maturity
- **Claude Code**: Plugin marketplace, MCP tool discovery, security hooks
- **OpenAI Codex**: MCP connection startup fallibility (#27261)
- **Gemini CLI**: MCP header encoding (#27771), atomic tool discovery (#27619)
- **Copilot CLI**: Custom registry URL construction (#3436), MCP server spawning loops (#3701)
- **Qwen Code**: Project-scoped `.mcp.json` with approval gates (#4615)
- **Common pain point**: All tools struggle with MCP server configuration fragility, OAuth handling, and discovery reliability

### C. Cross-Session Persistence & Memory
- **Claude Code**: Session JSONL data loss (#66734) — *regression showing fragility*
- **OpenAI Codex**: Chat history disappearance (#20741)
- **Gemini CLI**: Auto Memory retrying low-signal sessions (#26522)
- **Pi**: Session folder collision (#4877)
- **CodeWhale**: Hippocampal memory system proposal (#2935)
- **Common need**: Reliable, inspectable session persistence that survives updates and crashes

### D. Safety & Trust Systems
- **Claude Code**: Safety classifier false positives on legitimate content (#66728)
- **Gemini CLI**: Agent should discourage destructive git/DB operations (#22672)
- **OpenCode**: Sandboxing agent terminal commands (#2242)
- **Pi**: Project Trust feature with inheritable permissions (#5514)
- **Copilot CLI**: Worktree lifecycle management debate (#1613 vs #2243)
- **Common theme**: One-size-fits-all safety systems are failing; users want configurable, context-aware trust with clear opt-out paths

### E. Linux & Terminal UX
- **Claude Code**: Linux desktop build (#65697, 406👍 — highest open request)
- **Copilot CLI**: `ctrl+shift+c` broken on Linux (#2082)
- **Gemini CLI**: PTY resize crashes (#27496), terminal corruption (#24935)
- **OpenCode**: Copy/paste in CLI broken (#13984)
- **Pi**: CJK text wrapping (#5326), kitty keyboard support (#3967)
- **Common need**: First-class Linux support, consistent keyboard shortcuts, proper terminal emulation

### F. Provider & Model Flexibility
- **Claude Code → Amazon Bedrock**: Fable 5 Bedrock compatibility (#31560)
- **Pi**: Bedrock Mantle provider for OpenAI-compatible models (#5363)
- **OpenCode**: Custom provider options silently dropped (#5674)
- **CodeWhale**: Together AI + Qwen 3.7 Max support (#2925, #2927)
- **Common need**: Consistent behavior across providers, transparent error messages for incompatible features

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | CodeWhale |
|---|---|---|---|---|---|---|---|---|
| **Primary Model** | Fable 5 (Mythos) | gpt-5.5 | Gemini 3.5 Flash | Org-configured | Multi-provider | Multi-provider | Qwen 3.7+ | Multi-provider |
| **Target User** | Professional devs, enterprise | AI power users, pro subscribers | Google Cloud ecosystem | GitHub enterprise orgs | Self-hosted, privacy-conscious | TUI enthusiasts, hackers | Asian market, cloud-native | Cost-sensitive, token-conscious |
| **Key Differentiator** | Plugin ecosystem + safety hooks | Codex Desktop TUI + agent identity | Vertex AI integration + skills | GitHub ecosystem integration | Custom provider flexibility | Terminal aesthetics + speed | ACP protocol + Asian IME | Token efficiency discipline |
| **Risk Profile Today** | P0 data loss + safety regression | Model rollout failure | Agent hangs + misleading reporting | CLI parity abandonment | Memory leaks + provider bugs | Thinking mode incompatibility | CI pipeline failures | Rebrand migration friction |
| **Community Sentiment** | Frustrated but engaged | Frustrated (rollout pain) | Patient but concerned | Abandoned feeling (CLI fork exists) | Active but troubleshooting | Enthusiastic but bug-aware | Constructive, feature-hungry | Mixed (rebrand confusion) |

**Key differentiations:**

- **Claude Code** leads on plugin/extension ecosystem depth but is suffering from the most severe production bugs (data loss + safety miscategorization)
- **OpenAI Codex** is most aggressive on multi-agent infrastructure (agent identity, HAI stack) but has the worst rollout quality (gpt-5.5 404 affecting all users)
- **Gemini CLI** is strongest on Google Cloud integration but weakest on agent reliability (hangs, misleading success reporting)
- **Copilot CLI** is coasting on GitHub brand; community is actively forking (#53) due to perceived neglect
- **Pi** has the best TUI rendering quality focus but struggles with adaptive-thinking model compatibility
- **Qwen Code** is the most ambitious feature porter (Dynamic Workflows, Agent Teams, ACP) with the fastest iteration cadence
- **CodeWhale** is the most focused on token efficiency and prompt discipline, filling a niche others ignore

---

## 5. Community Momentum & Maturity

### High Momentum (Rapid Iteration, Growing Communities)
| Tool | Momentum Signal | Maturity Level |
|---|---|---|
| **Claude Code** | 10 PRs/day, major model launch, plugin ecosystem | **Mature** — largest community, most complex ecosystem, production-scale bugs |
| **OpenAI Codex** | 10 PRs/day, MultiAgentV2, HAI infrastructure | **Mature** — second-largest community, heavy enterprise use, steady feature velocity |
| **Qwen Code** | 10 PRs/day, multiple preview releases, ambitious feature ports | **Growth** — fastest iteration cycle, aggressive feature adoption from Claude Code |
| **Pi** | 10 PRs/day, v0.79.1 release, trust UX firestorm | **Growth** — active TUI-focused community, responsive maintainers |

### Steady State (Active Maintenance, Moderate Velocity)
| Tool | Momentum Signal | Maturity Level |
|---|---|---|
| **Gemini CLI** | 10 PRs/day, backported fixes, Vertex AI focus | **Established** — Google-backed, stable release cadence, but bug backlog growing |
| **OpenCode** | 10 PRs/day, memory megathread, provider fixes | **Established** — loyal self-hosting community, slow to resolve long-standing bugs |
| **CodeWhale** | 10 PRs/day, rebrand momentum, token efficiency push | **Emerging** — focused niche, rapid provider expansion, migration friction |

### Low Momentum (Maintenance Mode or Stalled)
| Tool | Momentum Signal | Maturity Level |
|---|---|---|
| **Copilot CLI** | 1 PR (low quality), 6-month-old CLI parity request | **Declining** — community forking, perceived neglect, minimal PR contribution |
| **Kimi Code CLI** | 1 PR, no release, 5-month-old bug unresolved | **Stalled** — minimal activity, unresolved critical bugs, low community engagement |

**Notable patterns:**
- **Claude Code's "Fable 5 launch" effect**: Highest spike in issues + PRs, but also highest severity regressions — typical for a major model transition
- **Copilot CLI's fork risk**: Issue #53 being actioned via community fork (`shell-ai`) is the strongest abandonment signal in the ecosystem
- **Qwen Code as "fastest feature porter"**: Landing Claude Code features (Dynamic Workflows, Plan Mode, MCP security) within 2-3 weeks of their Claude release — aggressive differentiation strategy
- **CodeWhale's niche positioning**: Token efficiency focus is unique — no other tool is systematically benchmarking against Codex's token usage (#2952-2962)

---

## 6. Trend Signals

### 1. The "Claude Code Diffusion Standard" is Emerging
Features introduced in Claude Code are being ported across the ecosystem within 2-6 weeks:
- **Dynamic Workflows** (JS sandbox + `agent()`): Already in Qwen Code (#4732), in progress for Codex and Gemini
- **Plan Mode**: Ported to Qwen Code (#4853)
- **Project-scoped MCP configs**: Appearing in Qwen Code (#4615), Copilot CLI (#3083)
- **Implication**: Claude Code is the de facto innovation leader; other tools are racing to achieve feature parity

### 2. Safety System Crisis is Universal
Every major tool faces a safety/trust tension:
- **Too aggressive**: Claude Code's classifier blocks legitimate syscall/ABI content; Gemini CLI's destructive command policies annoy power users
- **Too permissive**: CodeWhale's agent executes unrequested operations; Codex's gpt-5.5 rollout had no safety guardrails
- **Pattern**: The industry needs *configurable, transparent, context-aware* safety — not binary allow/block classifiers
- **Signal**: Pi's Project Trust inheritance model (#5549) is the most innovative safety UX in the ecosystem

### 3. Agent Reliability is the #1 Unmet Need
Despite rapid feature growth, basic reliability remains elusive:
- **Session data loss**: Claude Code (P0), Codex, Gemini all have active bugs
- **Agent hangs**: Gemini CLI (#21409), Codex (#26493)
- **Misleading status reporting**: Gemini CLI subagents report success on failure (#22323)
- **Pattern**: Tools are shipping features faster than they can stabilize core reliability
- **Implication**: The next competitive moat will be *reliability*, not feature count

### 4. MCP is Becoming a Standard, But It's Rough
MCP (Model Context Protocol) adoption is accelerating across all tools, but:
- **Discovery failures**: All tools report MCP server configuration as fragile
- **Security gaps**: Qwen Code (#4615) proposing approval gates; no tool has comprehensive MCP permissions
- **Performance overhead**: Gemini CLI's tool search caching (#27258) and Qwen's prefix stabilization (#4896) address caching issues introduced by MCP churn
- **Signal**: MCP will be the standard integration layer within 6 months, but tool vendors must invest in robust, secure, and performant implementations

### 5. Enterprise Demands are Driving Feature Priority
- **Model parity** (Copilot CLI #1703, Qwen Code #4904): Users expect same models in CLI as in IDE
- **Authentication robustness**: Session resume losing auth (Copilot CLI #3596), credential blob limits (Codex #17931)
- **Compliance features**: Project-scoped configs, persistent trust settings, audit trails
- **Signal**: Enterprise adoption is outpacing tool readiness; BYOK/self-hosted users face the worst experience

### 6. Token Efficiency is Becoming a Competitive Battleground
- **Codex**: Token efficiency regression (#27242) provoking Pro user backlash
- **CodeWhale**: Systematic benchmarking against Codex token usage (#2952-2962)
- **Qwen Code**: OOM prevention with explicit GC (#4914), prompt cache stabilization (#4896)
- **Pattern**: As model costs remain significant, token efficiency is becoming a key differentiator
- **Signal**: Tools that transparently report and optimize token usage will win cost-conscious developers

### 7. Community Forking is a Real Risk
- **Copilot CLI**: #53 spawned `shell-ai` fork — first verified community fork in the ecosystem
- **Reason**: 6+ months of silence on a 75-upvote request for CLI command parity
- **Implication**: Developer tool communities are pragmatic; if a company-abandoned feature blocks workflows, the community will build its own replacement
- **Warning signal**: Any tool that ignores top-10 issues for multiple releases risks fragmentation

---

## Summary for Technical Decision-Makers

| If you prioritize... | Lead tool | Runner-up |
|---|---|---|
| **Largest ecosystem + latest models** | Claude Code | OpenAI Codex |
| **Stability and reliability** | Pi | Gemini CLI |
| **Feature velocity** | Qwen Code | Pi |
| **Enterprise/GitHub integration** | Copilot CLI (declining) | OpenAI Codex |
| **Cost efficiency / token discipline** | CodeWhale | OpenCode (self-hosted) |
| **Custom providers / self-hosting** | OpenCode | Pi |
| **Google Cloud / Vertex AI** | Gemini CLI | — |
| **Multi-agent orchestration** | OpenAI Codex | Qwen Code |

**Risk-adjusted recommendation:** For production deployments today, **Pi** or **Gemini CLI** offer the best stability-to-feature ratio. **Claude Code** has the most advanced ecosystem but carries P0 data-loss risk. **Qwen Code** is the best bet for bleeding-edge features if you can tolerate preview-channel instability.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-06-10 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following pull requests have attracted the most community discussion and represent the most-watched skill development activity:

### #514 — Document Typography Skill *(Open)*
- **Functionality**: Prevents orphan word wrap (1–6 words on a new line), widow paragraph headers stranded at page bottom, and numbering misalignment in AI-generated documents.
- **Discussion Highlights**: Addresses a universal pain point—typographic quality in Claude-generated documents. Commenters noted this is a "silent quality issue" that affects every document but is rarely caught by users.
- **Status**: Open, with active discussion on edge cases for different output formats (PDF vs. DOCX vs. HTML).
- *Link*: [PR #514](https://github.com/anthropics/skills/pull/514)

### #486 — ODT Skill (OpenDocument Format) *(Open)*
- **Functionality**: Enables creation, template-filling, reading, and conversion of `.odt`/`.ods` files. Triggers on keywords like "ODT," "ODS," "LibreOffice."
- **Discussion Highlights**: High interest from enterprise users working in open-source document ecosystems. Several comments requested broader format support (ODP for presentations).
- **Status**: Open; the author has responded to feedback with incremental improvements.
- *Link*: [PR #486](https://github.com/anthropics/skills/pull/486)

### #210 — Frontend-Design Skill Clarity & Actionability *(Open)*
- **Functionality**: Revises the existing frontend-design skill so every instruction is actionable within a single Claude conversation, fixing internal consistency issues.
- **Discussion Highlights**: Community feedback focused on making skill instructions precise enough to steer behavior without over-constraining Claude's judgment. The PR serves as a model for skill quality standards.
- **Status**: Open with ongoing refinement.
- *Link*: [PR #210](https://github.com/anthropics/skills/pull/210)

### #83 — Skill-Quality-Analyzer & Skill-Security-Analyzer *(Open)*
- **Functionality**: Two meta-skills: one evaluates skills across structure, documentation, and examples; the other audits skills for security vulnerabilities and permission scoping.
- **Discussion Highlights**: Strong interest in meta-governance—the community wants tools to self-police skill quality. Security auditing was especially welcomed given later security concerns (see Issue #492).
- **Status**: Open, with requests for integration into CI/CD pipelines.
- *Link*: [PR #83](https://github.com/anthropics/skills/pull/83)

### #1140 — Agent-Creator Meta-Skill *(Open)*
- **Functionality**: Adds an agent-creator skill for task-specific agent sets, plus fixes for multi-tool evaluation and Windows support.
- **Discussion Highlights**: Represents a shift toward composable agents rather than monolithic skills. Commenters debated the UX of dynamically creating agent configurations.
- **Status**: Open, recently updated.
- *Link*: [PR #1140](https://github.com/anthropics/skills/pull/1140)

### #723 — Testing-Patterns Skill *(Open)*
- **Functionality**: Comprehensive testing skill covering the Testing Trophy model, AAA pattern, React component testing (Testing Library), Cypress E2E, and mocking strategies.
- **Discussion Highlights**: One of the most anticipated skills in the collection. Commenters requested additional coverage for Playwright and vitest.
- **Status**: Open; discussion around scope boundaries (should it include database testing?).
- *Link*: [PR #723](https://github.com/anthropics/skills/pull/723)

### #568 — ServiceNow Platform Skill *(Open)*
- **Functionality**: Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD/CSM, SPM, and IntegrationHub.
- **Discussion Highlights**: Enterprise demand is high. Commenters requested modular sub-skills for specific ServiceNow modules to avoid context bloat.
- **Status**: Open, with active revision.
- *Link*: [PR #568](https://github.com/anthropics/skills/pull/568)

### #538–#541 — Windows & Cross-Platform Compatibility Fixes *(Open)*
- **Functionality**: Three PRs fixing case-sensitive file references, YAML parsing validation, and DOCX tracked-change ID collisions.
- **Discussion Highlights**: These "fix" PRs are among the most-watched because they resolve blockers for entire user segments (Windows, file system edge cases).
- **Status**: Open, grouped as a compatibility push.
- *Links*: [PR #538](https://github.com/anthropics/skills/pull/538) | [PR #539](https://github.com/anthropics/skills/pull/539) | [PR #541](https://github.com/anthropics/skills/pull/541)

---

## 2. Community Demand Trends

From the top Issues, the community's most-anticipated new Skill directions are:

**🔒 Organizational & Security Features** (Issue #228, #492)
- **Org-wide skill sharing** (#228): 13 comments, 7 👍. Users want a shared skill library or direct sharing links instead of manual `.skill` file distribution via Slack/Teams.
- **Trust boundary concerns** (#492): 7 comments. Community skills distributed under the `anthropic/` namespace impersonate official skills, creating a permission-request trust vulnerability. Demand for namespace verification and provenance tracking.

**🛠 Tooling & Platform Support** (Issue #556, #1169, #202)
- **run_eval.py reliability** (#556): 11 comments. The evaluation pipeline never triggers skills (0% trigger rate), making skill optimization impossible. Critical for any skill developer.
- **skill-creator standardization** (#202): 8 comments. Call for the skill-creator skill itself to follow best practices—currently reads like developer docs rather than operational instructions.
- **Portability labeling** (#1156, #1220): Emerging demand for per-skill portability metadata and multi-file bundling to maintain complex reference-heavy skills.

**📄 Document & Format Expansion** (Issue #1175)
- **SharePoint Online support** (#1175): Security and context-window concerns when handling SPO documents via skills. Indicates enterprise demand for cloud document integration.

**🧪 Testing & QA** (Issue #412)
- **Agent governance** (#412): Safety patterns for AI agent systems—policy enforcement, threat detection, audit trails. This was closed but the topic continues in related discussions.

---

## 3. High-Potential Pending Skills

These PRs are actively discussed and likely to land soon:

| PR | Skill | Why It's High-Potential |
|----|-------|------------------------|
| #1140 | **agent-creator** | Meta-skill for composing task-specific agents; addresses composability demand. Recent updates (June 2). |
| #723 | **testing-patterns** | Fills a major gap in the collection; covers the full testing stack. |
| #568 | **servicenow** | Enterprise demand; large, well-structured submission with active maintainer. |
| #444 | **aurelion-kernel/advisor/agent/memory suite** | Four-skill cognitive framework suite (structured thinking, memory, task management). Sophisticated architecture. |
| #190 | **n8n-builder & n8n-debugger** | Workflow automation skills for n8n; popular automation platform. |
| #335 | **masonry-generate-image-and-videos** | AI image/video generation via Masonry CLI (Imagen, Veo). High appeal for creative workflows. |
| #154 | **shodh-memory** | Persistent context across conversations; addresses a core limitation of stateless AI interactions. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for platform-compatibility reliability and enterprise document handling**—the top discussions center on fixing the skill evaluation pipeline (run_eval.py, Windows support, YAML parsing) and extending document format support (ODT, typography, ServiceNow), reflecting a shift from experimental skill creation toward production-grade, cross-platform skill ecosystems that meet enterprise collaboration and security requirements.

---

# Claude Code Community Digest — 2026-06-10

## Today's Highlights

Anthropic released **Claude Fable 5**, a Mythos-class model described as their most capable ever, via version **v2.1.170** — but the launch is shadowed by a flood of reports about **safety classifier false positives** silently downgrading users mid-session. Separately, demand for a **native Linux desktop build** has surged to 407 upvotes in just five days, making it the highest-signal open feature request by a wide margin.

## Releases

**[v2.1.170](https://github.com/anthropics/claude-code/releases/tag/v2.1.170)** — Released today.

- **Claude Fable 5** (Mythos-class model) is now generally available. The post claims capabilities exceeding "any model ever made generally available." Access requires this update.
- Fixed a session-related bug (no further detail).

## Hot Issues (Top 10 by community signal)

1. **[#65697 — Official Linux desktop build](https://github.com/anthropics/claude-code/issues/65697)** — 406 👍, 31 comments, opened 5 days ago. The most upvoted open issue. Users want an official `.deb`/`.rpm` package for Ubuntu/Debian. Silent demand from the Linux developer community is extremely high.

2. **[#42776 — Desktop relaunch fails on Windows (file lock)](https://github.com/anthropics/claude-code/issues/42776)** — 86 comments, 31 👍. An orphaned process holds a file lock, preventing relaunch. Long-running (since April 2) and a daily pain for Windows users.

3. **[#52472 — Weekly usage limit resets early](https://github.com/anthropics/claude-code/issues/52472)** — 22 comments. Users report their weekly cap resets after 5 days instead of 7, causing lost quota. Affects macOS and VS Code. Trust issue for paying users.

4. **[#62699 — Can't copy text from Linux TUI](https://github.com/anthropics/claude-code/issues/62699)** — 10 comments, 7 👍. `Ctrl+Shift+C` and right-click context menus do not work in Claude Code's terminal UI on Linux. Blocks basic developer workflow.

5. **[#66728 — Fable 5 false-positive safety downgrade (syscall/ABI)](https://github.com/anthropics/claude-code/issues/66728)** — 3 comments, opened today. **P0-tagged**. The safety classifier incorrectly flags low-level system programming content, forces silent model downgrade from Fable 5 to Opus 4.8, breaking PR review workflows. Multiple duplicates (see #66641, #66671, #66674).

6. **[#66734 — Session JSONL data loss](https://github.com/anthropics/claude-code/issues/66734)** — 2 comments, opened today. Sessions since v2.1.168 are being rewritten to metadata-only stubs, permanently losing all user/assistant message records. `/resume` opens empty sessions. **Critical data-integrity bug**.

7. **[#66750 — Plugin marketplace uninstallable for never-launched users](https://github.com/anthropics/claude-code/issues/66750)** — 2 comments, opened today. If a user has never interactively launched `claude`, the official plugin marketplace is not registered, causing install/update failures. Blocks CI/CD and automated setups.

8. **[#62087 — CLAUDE.md guidelines repeatedly ignored](https://github.com/anthropics/claude-code/issues/62087)** — 6 comments. During long sessions, Claude Code systematically violates project-level CLAUDE.md rules despite them being in context. User must repeatedly catch and correct violations.

9. **[#66359 — Unattributable prompt injection](https://github.com/anthropics/claude-code/issues/66359)** — 4 comments, opened 2 days ago. A user reports suspected prompt injection and env-var exfiltration instructions appearing in a session after plugin installation. **Security concern**, source unknown.

10. **[#65989 — TUI cursor corruption on iOS SSH](https://github.com/anthropics/claude-code/issues/65989)** — 4 comments, 1 👍. Regression in v2.1.163: cursor desync and frame corruption in Secure ShellFish. Bisected to the specific version. Affects iOS developers.

## Key PR Progress

1. **[#66608 — Fix Fable 5 lattice gauge theory false positive](https://github.com/anthropics/claude-code/pull/66608)** — Automated fix via REAPR tool. Addresses a safety classifier false-positive on physics research content. Directly relevant to the Fable 5 launch issues.

2. **[#66607 — Fix Fable 5 auto-switch to Opus during security testing](https://github.com/anthropics/claude-code/pull/66607)** — Another REAPR automated fix for the same safety-classifier regression pattern as #66608.

3. **[#66650 — pr-review-toolkit author name fix](https://github.com/anthropics/claude-code/pull/66650)** — Corrects plugin manifest author from "Daisy" to "Daisy Hollman" for consistency with other bundled plugins.

4. **[#66577 — Sync security-guidance plugin marketplace metadata](https://github.com/anthropics/claude-code/pull/66577)** — Fixes out-of-sync version (1.0.0 → 2.0.0) and description between marketplace.json and plugin.json for the security-guidance hook.

5. **[#66575 — pr-review-toolkit plugin.json author fix](https://github.com/anthropics/claude-code/pull/66575)** — Same author consistency fix as #66650 but in the plugin's own `plugin.json`.

6. **[#66573 — Fix ralph-wiggum error handlers broken by set -euo pipefail](https://github.com/anthropics/claude-code/pull/66573)** — Critical fix: `set -euo pipefail` was causing the hook script to silently exit before reaching error-handling code, masking failures.

7. **[#66572 — WIP: Fix repeated "Image couldn't be processed" API errors](https://github.com/anthropics/claude-code/pull/66572)** — Work-in-progress addressing a bug that consumes usage limits via repeated image-processing failures. Still needs testing.

8. **[#66416 — Fix plugin-dev validator scripts aborting on first finding](https://github.com/anthropics/claude-code/pull/66416)** — Three validator scripts abort at the first error due to `set -e`, preventing comprehensive validation output. Simple but impactful fix.

9. **[#65723 — Claude/subscription debate chat rx ewi](https://github.com/anthropics/claude-code/pull/65723)** — No description provided. Low-signal PR; appears to be a stray or experimental submission.

10. **[#66650 — (listed above)](https://github.com/anthropics/claude-code/pull/66650)** — Already covered; noted for completeness on plugin-ecosystem improvements.

## Feature Request Trends

- **Linux native support** (#65697, 406👍) — Dominant request. Desktop app + CLI parity for Ubuntu/Debian.
- **Localization/i18n** (#66743, #66637) — Multiple requests for Korean (ko-KR) and Portuguese (pt-BR) UI support, including permission prompts.
- **Session-only model persistence** (#63413) — Users want `/model <name>` to support a session-only flag, not force global settings persistence.
- **Claude Desktop deep linking** (#54614) — Request to launch Code sessions rooted at specific folders via CLI flag or deep link.
- **Assistant text output hooks** (#37243, closed but high engagement) — Users want `PreResponse`/`PostResponse` hooks to enforce behavioral rules on text output, currently only tool calls are hookable.

## Developer Pain Points

1. **Fable 5 safety classifier false positives** — Multiple open bugs (#66728, #66641, #66671, #66674, #66744) report that the safety system silently downgrades the model or blocks legitimate technical, academic, and domain-specific content. **This is the #1 friction point today.**

2. **Session data loss** (#66734) — A severe data-integrity regression affecting v2.1.168–170. Sessions are being truncated to metadata stubs, with permanent loss of conversation history.

3. **Windows reliability issues** — Two distinct bugs (#42776, #53247) prevent desktop relaunch after crashes due to orphaned process locks and Job Object issues. Recovery requires reboot or logoff.

4. **CLAUDE.md guideline non-compliance** (#62087) — During long sessions, project rules are systematically violated, requiring constant user supervision. Undermines trust in autonomous coding.

5. **Plugin ecosystem friction** — Marketplace registration (#66750), plugin metadata drift (#66577), and shell-script `set -e` bugs (#66573, #66416) show that the plugin system still has rough edges for both users and developers.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-10

## Today's Highlights
The community remains heavily impacted by a widespread `gpt-5.5` rollout failure (#26892, 79 comments) where the model appears available but returns 404 on both Desktop and CLI — the top issue by far. Meanwhile, multiple releases landed today, including `rust-v0.139.0` with standalone web search from nested tool calls, and internal infrastructure PRs are focused on reducing CPU spikes during archive operations and caching tool search handlers across sampling continuations. Persistent session history display bugs on Windows and macOS continue to generate substantial discussion.

## Releases
**rust-v0.139.0** (released today):
- Code mode can now call standalone web search directly, including from nested JavaScript tool calls, and receive plaintext search results (#26719)
- Tool and connector input schemas now preserve `oneOf` and `allOf`; large schemas keep more shallow structure when compacted

**Pre-release builds** also published: `rust-v0.140.0-alpha.2`, `rust-v0.139.0-alpha.3`, `rust-v0.139.0-alpha.2`

## Hot Issues

1. **[#26892] gpt-5.5 is listed as available locally but real requests fail with 404** (79 comments, 28 👍) — The top community pain point. Model metadata shows `gpt-5.5` as available across Desktop and CLI on multiple platforms, but actual API calls return 404. Several duplicate reports exist (#26910, #27021, #26916, #26927). Appears to be a server-side rollout issue rather than client bug.
   https://github.com/openai/codex/issues/26892

2. **[#20741] Codex Desktop project chat histories disappeared after update** (32 comments, 14 👍) — Long-standing issue affecting macOS Tahoe users. After updating, project chat histories vanish from the sidebar though local session files remain. Community is frustrated by the lack of a resolution after over a month.
   https://github.com/openai/codex/issues/20741

3. **[#25500] Projects sidebar shows "No chats" for projects with older non-archived conversations** (16 comments, 2 👍) — Related to #20741 but possibly a distinct bug. Windows users report that existing conversations appear in the filesystem but the UI fails to enumerate them. Updated today.
   https://github.com/openai/codex/issues/25500

4. **[#26493] Context compaction fails with `invalid_enum_value` for `context_compaction`** (16 comments, 4 👍) — Affects Windows and Remote SSH users. The app attempts to compact context but sends an invalid enum value, crashing the session. A community workaround was proposed in #27267.
   https://github.com/openai/codex/issues/26493

5. **[#27242] Codex is burning weekly limits much faster: token efficiency regression** (3 comments, 0 👍) — New but potentially explosive. Pro users report that completing the same dev tasks now consumes significantly more tokens. If validated, this represents a serious regression in model efficiency.
   https://github.com/openai/codex/issues/27242

6. **[#25004] Pet display flickers in Windows Terminal + WSL2** (9 comments, 0 👍) — A minor but persistent UI bug. The Codex CLI "pet" character flickers constantly in Windows Terminal under WSL2, making the TUI unpleasant for daily use.
   https://github.com/openai/codex/issues/25004

7. **[#24564] White screen of death - Codex extension starts and then crashes immediately** (6 comments, 0 👍) — Affects Linux aarch64 users specifically. The VS Code extension crashes at startup with no recovery path.
   https://github.com/openai/codex/issues/24564

8. **[#16717] Configurable Windows agent shell (PowerShell/git-bash)** (8 comments, 15 👍) — A high-engagement enhancement request. PowerShell syntax is poorly understood by models compared to bash. Users want a config key to switch to Git Bash or other shells.
   https://github.com/openai/codex/issues/16717

9. **[#26753] MultiAgentV2 encrypted spawn_agent schema returns 400** (6 comments, 1 👍) — Upgrading to current alpha CLI with `multi_agent_v2` enabled breaks every turn. The encrypted tool schema is rejected by the server, blocking all prompts even without sub-agent usage.
   https://github.com/openai/codex/issues/26753

10. **[#25231] Windows Codex Desktop notification click launches Electron error** (8 comments, 0 👍) — Clicking a Windows toast notification opens an Electron error dialog instead of the Codex app. Core UX broken for Windows users.
    https://github.com/openai/codex/issues/25231

## Key PR Progress

1. **[#27276] Reduce archive rollout lookup CPU** (new today) — Addresses CPU spikes during thread archiving by preferring UUID-based file lookup over exhaustive DB scans. Important for app-server stability at scale.
   https://github.com/openai/codex/pull/27276

2. **[#27258] Cache tool search handler across sampling continuations** (new today) — Rebuilds the deferred-tool BM25 search index only when tools actually change, rather than before every continuation. Aims to eliminate ~113ms per continuation overhead.
   https://github.com/openai/codex/pull/27258

3. **[#27261] Make MCP connection startup fallible** (new today) — Refactors MCP connection initialization to avoid exposing internal manager state purely for validation. Makes startup failure handling more robust.
   https://github.com/openai/codex/pull/27261

4. **[#25232] Derive window generation from effective rollout lineage** (closed today) — Fixes `x-codex-window-id` generation after rollback, resume, and fork scenarios. Ensures context window identification is deterministic across session recovery.
   https://github.com/openai/codex/pull/25232

5. **[#27078] Emit goal lifecycle analytics** (closed today) — Adds analytics events for `/goal` behavior. Enables tracking goal execution and outcomes, addressing a blind spot in observability.
   https://github.com/openai/codex/pull/27078

6. **[#17931] Support encrypted local secrets for keyring auth** (updated today) — Workaround for Windows Credential Manager's 2,560-byte blob limit. Large ChatGPT auth payloads and MCP OAuth tokens can now be stored securely even when they exceed this limit.
   https://github.com/openai/codex/pull/17931

7. **[#19047 / #19049 / #19051] Agent Identity / HAI single-run-task stack** (updated today, 3 PRs) — A multi-PR effort adding agent identity assertion, task-registration primitives, and inference auth. This enables "simplified HAI" where a single run-task handles authentication across agents. Still open after ~7 weeks.
   https://github.com/openai/codex/pull/19047

8. **[#27127] Forward assistant output to realtime through handoffs** (new today) — Ensures realtime voice feels like one coherent assistant by forwarding all user-facing Codex messages (preambles, finals) through handoff boundaries, regardless of input modality.
   https://github.com/openai/codex/pull/27127

9. **[#25158] Support more Vim normal commands** (updated today) — Adds `gg`/`G`, `dG`, `yG`, `dgg`, `cG`/`cgg`, and characterwise visual mode to the composer editor. Direct response to developer demand for better Vim emulation.
   https://github.com/openai/codex/pull/25158

10. **[#27122] Consolidate Responses API Codex metadata** (new today) — Introduces a canonical `CodexResponsesMetadata` struct for all metadata sent to Responses API. Standardizes fields like `thread_id`, `turn_id`, `window_id` under `x-codex-turn-metadata`.
    https://github.com/openai/codex/pull/27122

## Feature Request Trends

- **Multi-root workspace support** (#2909, 125 👍, open since Aug 2025) — The single most upvoted feature request. Developers using VS Code multi-root workspaces cannot use Codex effectively because the extension doesn't understand the workspace structure.
- **Export entire session** (#13267, 7 👍) — Users want a `/export` command for full session export from the TUI.
- **`codex models` CLI command** (#23279) — A simple CLI command to list available models, indicating friction in model discovery.
- **`spawn_agent` `cwd` support** (#18969, #23095, combined 8 👍) — Multiple requests for the ability to specify working directories when spawning subagents, particularly for parallel worktree operations.
- **Configurable Windows agent shell** (#16717, 15 👍) — Strong community desire to escape PowerShell syntax limitations.

## Developer Pain Points

- **gpt-5.5 404 rollout failure** (5+ separate issue threads, 79+ comments on the main thread) — The top blocker. Model appears locally but fails server-side. Affects all platforms and regions.
- **Session history disappearing** (#20741, #25500, #22796, #27243) — A cluster of related bugs where the UI shows "No chats" despite valid session files on disk. Particularly acute on Windows with `\\?\` path prefix issues and cloud sync.
- **Context compaction enum errors** (#26493, #27267) — Sessions break when the app sends invalid enum values during compaction. Community is patchworking workarounds.
- **Token efficiency regression** (#27242) — If validated, this makes Pro usage limits feel insufficient, undermining the value proposition of paid plans.
- **Windows-specific UX pain** (#25231 notifications broken, #20858 CWD mismatch, #25004 flickering pet) — Windows users consistently face more bugs than macOS/Linux users, spanning system integration, terminal behavior, and UI rendering.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-10

## Today's Highlights

A flurry of patch releases landed today, with **v0.47.0-preview.0**, **v0.46.0**, **v0.46.0-preview.3**, and **v0.45.3** all shipping within the last 24 hours. The standout fix is a backported Vertex AI model mapping correction that resolves authentication issues for non-AI Studio users. Meanwhile, the community continues to report agent hangs, subagent misreporting, and concerns around subagent autonomy—three of the seven most-discussed open issues.

## Releases

**v0.47.0-preview.0** (nightly) — Changelog PR [#27776](https://github.com/google-gemini/gemini-cli/pull/27776). Key change: "Respect backend def" — likely related to improved backend configuration handling for model routing.

**v0.46.0** (stable) — Includes fix `fix(core): harden PTY resize against native crashes` ([#27496](https://github.com/google-gemini/gemini-cli/pull/27496)), which should reduce terminal corruption on resize, plus changelogs for prior preview releases.

**v0.46.0-preview.3** & **v0.45.3** — Both are cherry-pick patches of commit `f08b4af` from PR [#27749](https://github.com/google-gemini/gemini-cli/pull/27749). This commit refactors Vertex AI model mapping for `gemini-3.5-flash`, ensuring non-AI-Studio auth types (COMPUTE_ADC, LOGIN_WITH_GOOGLE) correctly route requests without hitting the wrong model ID.

Full changelogs: [v0.47.0-preview.0](https://github.com/google-gemini/gemini-cli/compare/v0.46.0-preview.3...v0.47.0-preview.0), [v0.46.0](https://github.com/google-gemini/gemini-cli/compare/v0.45.0...v0.46.0), [v0.46.0-preview.3](https://github.com/google-gemini/gemini-cli/compare/v0.46.0-preview.2...v0.46.0-preview.3), [v0.45.3](https://github.com/google-gemini/gemini-cli/compare/v0.45.2...v0.45.3).

---

## Hot Issues

1. **[Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8👍, 7 comments) — One of the highest-upvoted bugs. Simple operations like folder creation cause indefinite hangs when the CLI defers to the generalist agent. Workaround: instructing the model not to use subagents. **Why it matters**: Core reliability issue affecting basic workflow completion.

2. **[Subagent recovery after MAX_TURNS reports GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 2👍, 6 comments) — `codebase_investigator` subagent returns `status: "success"` / `Termination Reason: "GOAL"` even after hitting the turn limit without doing any analysis. **Why it matters**: Undermines trust in agent reporting; users cannot distinguish real success from silent failures.

3. **[Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments) — Custom skills (e.g., gradle, git) are ignored unless explicitly invoked by the user. **Why it matters**: Diminishes the ROI of skill authoring and reduces autonomy for repetitive tasks.

4. **[Shell command gets stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 3👍, 4 comments) — Simple CLI commands hang with "Awaiting user input" even after the command finished. **Why it matters**: Directly blocks shell-driven agent workflows, a core use case.

5. **[Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, 1👍, 4 comments) — Browser agent crashes or reports GOAL failure under Wayland display servers. **Why it matters**: Linux users (increasingly Wayland-native) cannot rely on browser automation.

6. **[Thinking bug — 7+ minute waits](https://github.com/google-gemini/gemini-cli/issues/27766)** (P2, 3 comments, filed yesterday) — Fresh report: the agent "stuck on thinking" for 7 minutes on a normally 1–2 minute task. **Why it matters**: New symptom suggesting either model-side latency or tool-loop regression.

7. **[400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, 3 comments) — API rejects requests when tool count exceeds 128, with no smart tool-scoping by the agent. **Why it matters**: Power users with many MCP tools or skills hit a hard ceiling.

8. **[Model creates temp scripts in random spots](https://github.com/google-gemini/gemini-cli/issues/23571)** (P2, 3 comments) — When restricted from shell execution, the model scatters edit scripts across directories, creating cleanup burden. **Why it matters**: Workflow hygiene for commit readiness.

9. **[Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments) — Sessions that the extraction agent decides to skip remain unprocessed and are continuously re-surfaced. **Why it matters**: Wastes API quota and memory-background-processing cycles.

10. **[Agent should discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, 1👍, 2 comments) — The model uses `git reset` or `--force` when safer alternatives exist, risking data loss. **Why it matters**: Safety concern for production codebases.

---

## Key PR Progress

1. **[Avoid persisting empty resume sessions](https://github.com/google-gemini/gemini-cli/pull/27770)** (🎉 Merged) — Filters command-only and empty interactive sessions from resume flows. Prevents "started and quit immediately" from polluting session history.

2. **[Vertex AI model mapping fix](https://github.com/google-gemini/gemini-cli/pull/27749)** (🎉 Merged) — Refactors model ID routing for `gemini-3.5-flash` under LOGIN_WITH_GOOGLE and COMPUTE_ADC auth. Backported into v0.46.0-preview.3 and v0.45.3.

3. **[Standardize tool output formatting](https://github.com/google-gemini/gemini-cli/pull/27772)** (🔄 Open) — Introduces `wrapUntrusted` helper to unify text formatting from MCP, shell, and web-fetch tools. Reduces code duplication and ensures consistent data structures.

4. **[Prevent path traversal during skill install/link/uninstall](https://github.com/google-gemini/gemini-cli/pull/27767)** (🔄 Open) — Mitigates three path-traversal vulnerabilities in skill frontmatter parsing. Uses path normalization and directory-scope checks.

5. **[Fix MCP header encoding for non-ASCII values](https://github.com/google-gemini/gemini-cli/pull/27771)** (🔄 Open, P2) — Encodes Unicode header values (e.g., `mąka`) as `ByteString` so MCP HTTP discovery doesn't fail. Fixes [#25668](https://github.com/google-gemini/gemini-cli/issues/25668).

6. **[Fix internal session context from history during resumption](https://github.com/google-gemini/gemini-cli/pull/27391)** (🎉 Merged) — Filters internal `<session_context>` blocks from displayed TUI history, cleaning up resume experience.

7. **[Promote Gemini 3.1 Flash Lite to GA + support 3.5 Flash](https://github.com/google-gemini/gemini-cli/pull/27705)** (🔄 Open, size/xl) — Major model update: replaces preview model IDs with stable GA models. Unifies model promotion across AI Studio and Vertex AI.

8. **[Atomic update in MCP tool discovery](https://github.com/google-gemini/gemini-cli/pull/27619)** (🎉 Merged) — Prevents "tool not found" errors during transient network drops by retaining last-known-good tool registry during refresh failures.

9. **[Use gemini-3.5-flash for all auth types including Vertex AI](https://github.com/google-gemini/gemini-cli/pull/27760)** (🔄 Open, P1, help wanted) — Follow-up to PR 27749: ensures `setFlashModels()` correctly sets `gemini-3.5-flash` for Vertex AI auth, not just AI Studio.

10. **[Fail fast on zero-quota limits](https://github.com/google-gemini/gemini-cli/pull/27698)** (🔄 Open) — Prevents 10-attempt retry loop when hitting a `0` quota limit (e.g., unbilled accounts). Returns error immediately instead of wasting attempts.

---

## Feature Request Trends

**1. Smarter Agent Orchestration** — Multiple issues request improvements to when and how the agent delegates to subagents: better tool-scoping when >128 tools are available ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)), more autonomous skill usage ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)), and respecting `settings.json` overrides for browser agent maxTurns ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)).

**2. AST-Aware Tools** — Two related epics ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) investigate using Abstract Syntax Tree tools for file reads, search, and codebase mapping. Goal: more precise method-bound detection, fewer misaligned reads, and reduced token noise.

**3. Agent Safety and Self-Awareness** — Users want agents to understand their own CLI flags, hotkeys, and capabilities ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)), and to avoid destructive git/DB commands ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)). Two complementary directions: tool usage safety and meta-cognitive self-limitation.

**4. Browser Agent Resilience** — Requests for automatic session takeover and lock recovery ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)), plus persistent browser-settings override support ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), indicate growing demand for reliable browser automation.

**5. Remote Agents with Advanced Auth** — Epic [#20303](https://github.com/google-gemini/gemini-cli/issues/20303) (P1) covers task-level authentication, first-party agent support, and background processing for remote agent execution.

---

## Developer Pain Points

**🔴 Agent Hang / Infinite Loop (Highest Pain)** — Three distinct issues: generalist agent hanging ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell command stuck on "Waiting input" ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and new "thinking bug" with 7+ minute stalls ([#27766](https://github.com/google-gemini/gemini-cli/issues/27766)). This is the single largest category of user frustration.

**🔴 Misleading Agent Status Reporting** — Subagents reporting `success`/`GOAL` despite hitting turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) erodes trust. Users cannot distinguish successful completions from silently interrupted ones.

**🔴 Unwanted Subagent Autonomy** — Subagents activating despite being disabled in configuration ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) and overriding settings.json ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)). Users want explicit opt-in control.

**🔴 Terminal UI Corruption** — Issues with PTY resize crashes ([#27496](https://github.com/google-gemini/gemini-cli/pull/27496) — fixed in v0.46.0), corruption after exiting external editors ([#24935](https://github.com/google-gemini/gemini-cli/issues/24935)), and flicker/performance on resize ([#21924](https://github.com/google-gemini/gemini-cli/issues/21924)). Terminal stability remains a consistent concern.

**🟡 Memory & Session Hygiene** — Auto Memory retrying low-signal sessions ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), invalid patches being silently skipped ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)), and command-only sessions polluting resume history ([#27770](https://github.com/google-gemini/gemini-cli/pull/27770) — now fixed). Background extraction reliability needs more attention.

**🟡 Security: Path Traversal in Skills** — Two PRs ([#27659](https://github.com/google-gemini/gemini-cli/pull/27659), [#27767](https://github.com/google-gemini/gemini-cli/pull/27767)) fix path-traversal vulnerabilities in skill install/link/uninstall. This is a security-critical area that has received multiple fixes in quick succession.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-06-10

---

## 1. Today's Highlights

The community's long-standing demand for CLI command parity with the original `github copilot` alias continues to simmer, with Issue #53 accumulating 75 upvotes and spawning community-maintained forks. A new release v1.0.61 landed yesterday, bringing polished settings dialogs and critical bug fixes for session resuming and blank screens, but it has also introduced fresh concerns around BYOK model behavior and non-UTF-8 file corruption. Developer frustration is mounting around model inconsistency between Copilot CLI and VS Code, MCP server connectivity regressions, and Linux keyboard shortcuts being broken.

---

## 2. Releases

**v1.0.61** (2026-06-09)

- **Polish:** `/agents` picker and "Create New Agent" wizard now have consistent borders, headers, and styled inputs.
- **New feature:** `/settings` interactive dialog allows browsing and editing all user settings in one place.
- **Bug fix:** Resuming a session no longer leaves the screen blank.
- **Bug fix:** Resuming a local session with [additional fixes not fully detailed in changelog].

> No breaking changes or deprecation notices were included in this release.

---

## 3. Hot Issues

| # | Issue | Why It Matters | Community Reaction |
|---|-------|----------------|-------------------|
| [#53](https://github.com/github/copilot-cli/issues/53) | Bring back `github copilot` CLI commands | After 6+ months of silence, the community has forked the tool (`shell-ai`). 75 upvotes, 31 comments — the highest-signal grievance in the repo. | High urgency; users feel abandoned |
| [#1703](https://github.com/github/copilot-cli/issues/1703) | Copilot CLI doesn't list all org-enabled models (e.g. Gemini 3.1 Pro) | Models available in VS Code are missing in CLI for the same org/account. Breaks enterprise workflows. | 54 👍, 29 comments; heavy push for parity |
| [#2082](https://github.com/github/copilot-cli/issues/2082) | `ctrl+shift+c` no longer copies on Linux | A standard terminal shortcut broken since v1.0.4. Affects all Ubuntu 24.04 users. | 8 👍, 20 comments; widespread frustration |
| [#3596](https://github.com/github/copilot-cli/issues/3596) | "Not authenticated" error when resuming sessions | Users must start a new session to list models — a clear resume-path regression. | 10 👍, 3 comments; affects daily workflow |
| [#1613](https://github.com/github/copilot-cli/issues/1613) | Feature request: Built-in git worktree lifecycle management | High demand (31 👍) for Copilot to create/destroy worktrees during task solving. | Strong community interest; seen as safety improvement |
| [#2243](https://github.com/github/copilot-cli/issues/2243) | Worktrees should be disabled by default | Opposite perspective: worktrees cause chaos with thousands of lines of code that can’t be merged back. | 8 👍, 2 comments; polarizing topic |
| [#3436](https://github.com/github/copilot-cli/issues/3436) | `/mcp search` constructs wrong URL for custom MCP registries | Missing `/v0.1/` segment causes 404s for self-hosted registries. Enterprise blocker. | 1 👍, 7 comments; niche but critical for org deployments |
| [#3701](https://github.com/github/copilot-cli/issues/3701) | Runaway MCP server spawning loop on Windows | IDE lock-file watcher triggers re-init loop. Performance hazard for multi-workspace users. | 0 👍, 4 comments; reported on both WinGet and VS Code |
| [#3736](https://github.com/github/copilot-cli/issues/3736) (NEW) | Thinking tokens never appear with BYOK models | Users of bring-your-own-key models see no "Thinking..." text regardless of endpoint type. | Fresh; zero comments but filed against v1.0.61 |
| [#3732](https://github.com/github/copilot-cli/issues/3732) (NEW) | `edit` tool corrupts non-UTF-8 bytes | Files with legacy single-byte encodings (e.g. CP1252) are silently corrupted. Data integrity issue. | Fresh; zero comments; high severity for legacy codebases |

---

## 4. Key PR Progress

Only one PR was updated in the last 24 hours:

| # | PR | Status | Description |
|---|-----|--------|-------------|
| [#3737](https://github.com/github/copilot-cli/pull/3737) | Jigg empire ai | OPEN | Low-quality test PR ("Let’s try this new method"). No substantive code changes. |

> **Note:** The PR pipeline is unusually quiet today. The community is primarily discussing bugs and feature requests in Issues rather than contributing patches.

---

## 5. Feature Request Trends

The following directions are most-requested across open Issues:

1. **CLI Command Parity** — Restoring the original `github copilot` alias to avoid breaking scripts/CI workflows. (#53)
2. **Enterprise Model Support** — Full model list parity with VS Code, including BYOK and custom admin-managed models. (#1703, #3730)
3. **MCP Ecosystem Maturity** — Automatic MCP server loading from config files, custom registry support with correct URL paths, and OAuth rate-limit mitigation. (#3436, #3548, #3706)
4. **Git Worktree Lifecycle Management** — Native support for creating/destroying worktrees during agent sessions, with safe defaults and user toggle. (#1613, #2243)
5. **Session Mobility** — Share local sessions across multiple machines/instances. (#3729)

---

## 6. Developer Pain Points

- **Model Inconsistency:** Models enabled in GitHub org settings appear in VS Code but not in Copilot CLI (#1703). This creates confusion and workflow breaks for enterprise users.
- **Authentication State Loss:** Resuming a session can lose authentication context, preventing model listing (#3596). A significant usability regression.
- **Keyboard Shortcut Breakage on Linux:** `ctrl+shift+c` for clipboard copy has been broken since v1.0.4 (#2082). Combined with `ctrl+wheel` zoom being blocked on Windows (#3735), input handling is a recurring sore point.
- **MCP Server Configuration Fragility:** Custom registry URLs can 404 (#3436), MCP servers fail to auto-load from `.mcp.json` (#3083), and remote MCP OAuth triggers runaway re-initialization (#3706).
- **File Encoding and Data Corruption:** The `edit` tool corrupts non-UTF-8 bytes (#3732), and the bash tool strips non-ASCII characters (#3601). For international development teams, this is a blocker.
- **Plugin Hook Regression:** The `userPromptSubmitted` hook's `additionalContext` no longer injects into the planner in v1.0.60 (#3727), breaking plugin-based customization workflows.

---

*Digest generated from github.com/github/copilot-cli activity ending 2026-06-10.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest**
**Date:** 2026-06-10

**1. Today's Highlights**
No new releases were published in the last 24 hours. The community spotlight falls on a high-impact PR that improves LLM context visibility by making the PostToolUse hook awaitable, and on a long-running, niche bug involving file-reading loops on Arch Linux. A new issue also reports persistent edit tool failures in the latest Kimi Code v0.12.0, indicating possible regressions.

**2. Releases**
None in the last 24 hours.

**3. Hot Issues**

1.  **[#640] [bug] Kimi CLI stuck in reading one file again and again and stuck in a loop**
    - **Summary:** A user on Arch Linux reports that Kimi CLI 0.76 with a custom Anthropic endpoint (model mimo-v2-flash) enters an infinite loop reading the same file. The issue has been open since January, with 7 comments and low engagement (1👍).
    - **Why it matters:** This is a critical usability bug affecting a specific but non-trivial configuration (custom endpoints, Arch Linux); it remains unresolved after 5 months.
    - [GitHub Issue #640](https://github.com/MoonshotAI/kimi-cli/issues/640)

2.  **[#2443] [bug] Edit tool keeps failing in new kimi-code**
    - **Summary:** Running Kimi Code v0.12.0 on Debian with the k2.6 model, a user reports frequent failures during the edit tool phase, with errors appearing in the output.
    - **Why it matters:** This suggests a potential regression in v0.12.0's core editing workflow, which is used for code modification.
    - **Community reaction:** No comments or upvotes yet (fresh issue from yesterday).
    - [GitHub Issue #2443](https://github.com/MoonshotAI/kimi-cli/issues/2443)

**4. Key PR Progress**

1.  **[#2445] feat(hooks): surface PostToolUse hook stderr to LLM context**
    - **Author:** zwpdbh
    - **Summary:** Converts the PostToolUse hook from fire-and-forget to an awaited task; hook stderr is now collected and appended to the tool result message, giving the LLM immediate visibility into hook output.
    - **Why it matters:** This is a foundational improvement for agentic debugging and observability—hooks no longer operate in the dark.
    - **Community reaction:** No comments yet; open for less than 24 hours.
    - [GitHub PR #2445](https://github.com/MoonshotAI/kimi-cli/pull/2445)

**5. Feature Request Trends**
Based on the most recent issues and PRs, the current feature request landscape shows a clear emphasis on **observability and debuggability of tool execution** (e.g., surfacing hook stderr to the LLM). There is also an emerging demand for **better error resilience** in the edit tool workflow, especially in the latest CLI versions.

**6. Developer Pain Points**
- **Edit tool reliability:** The new Kimi Code v0.12.0 shows edit tool failures on Debian, which is a critical workflow blocker.
- **Stuck/long-running loops:** A persistent issue (#640) affecting custom endpoints and Arch Linux demonstrates pain around execution control and file-handling loops.
- **Low visibility of hook outputs:** The community is actively addressing the lack of feedback from PostToolUse hooks, though this is being mitigated by PR #2445.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-10

## Today's Highlights
The community remains actively engaged despite no new releases, with the ongoing **Memory Megathread** and **sandboxing demands** dominating discussion. A critical **prompt loop cache-busting bug** (#31525) was surfaced alongside a cluster of fixes landing for **tool_use/tool_result integrity** (#31547) and **filesystem search unification** (#31566). Several **custom provider issues** continue to frustrate users, particularly around image attachments and streaming tool calls.

## Releases
No new versions were published in the last 24 hours.

## Hot Issues

**1. Memory Megathread** [#20695](https://github.com/anomalyco/opencode/issues/20695)
*91 comments, 64 👍* — Central hub for memory leak reports. Maintainers explicitly ask for heap snapshots, not LLM-suggested fixes. High activity suggests ongoing stability concerns.

**2. Sandboxing the Agent** [#2242](https://github.com/anomalyco/opencode/issues/2242)
*64 comments, 53 👍* — Long-running request for terminal command sandboxing (like macOS seatbelt). No solution in sight; community interest remains high.

**3. Copy/Paste in CLI** [#13984](https://github.com/anomalyco/opencode/issues/13984)
*45 comments, 20 👍* — Persistent clipboard issue across platforms. Users report "copied to clipboard" toast but paste yields nothing.

**4. Context Awareness Not Working** [#3472](https://github.com/anomalyco/opencode/issues/3472) *(CLOSED)*
*38 comments, 26 👍* — VSCode extension claims context awareness but selected lines are invisible to the agent. Documentation gap suspected.

**5. Custom Provider Options Not Passed** [#5674](https://github.com/anomalyco/opencode/issues/5674)
*23 comments, 13 👍* — `baseURL` and `apiKey` from custom OpenAI-compatible providers silently dropped. Blocks self-hosted setups.

**6. Image Attachments Fail for Custom Providers** [#20802](https://github.com/anomalyco/opencode/issues/20802)
*15 comments, 7 👍* — Vision-capable models don't receive image input via custom providers, though same provider works outside OpenCode.

**7. Prompt Loop Reloads All Messages Every Iteration** [#31525](https://github.com/anomalyco/opencode/issues/31525)
*4 comments* — Fresh bug: `filterCompactedEffect` reloads DB rows each loop, breaking Anthropic's prompt cache byte-identity. Performance and cost impact for heavy users.

**8. Tool Execution Aborted** [#18757](https://github.com/anomalyco/opencode/issues/18757)
*5 comments* — Tools (bash, edit, read) intermittently fail with "Tool execution aborted" in v1.3.0. Requires session restart.

**9. Fable 5 + Bedrock Unsupported Parameter** [#31560](https://github.com/anomalyco/opencode/issues/31560) *(CLOSED)*
*3 comments, 1 👍* — New Fable 5 model broken on Bedrock due to `data retention mode 'default'` field being sent. Quick close suggests known fix.

**10. vLLM Tool Call Streaming Breaks** [#26412](https://github.com/anomalyco/opencode/issues/26412)
*3 comments* — Custom vLLM providers fail with `Expected 'function.name' to be a string` on streaming tool calls. Blocks many self-hosted deployments.

## Key PR Progress

**1. iFlow Provider for Web Tools** [#31515](https://github.com/anomalyco/opencode/pull/31515)
Opt-in provider for `websearch`/`webfetch` via iFlow API.

**2. TUI Question Dialog Fix** [#28936](https://github.com/anomalyco/opencode/pull/28936)
Prevents question prompts from hijacking the "open" dialog in TUI.

**3. CLI Error Output Fix** [#31591](https://github.com/anomalyco/opencode/pull/31591)
`.fail()` handler now actually shows yargs error messages instead of help text.

**4. Orphan Session Preservation** [#30682](https://github.com/anomalyco/opencode/pull/30682)
Preserves sessions when git history rewrite changes project ID.

**5. V2 Filesystem Search for Pickers** [#31589](https://github.com/anomalyco/opencode/pull/31589)
Migrates shared pickers from legacy find endpoint to v2.fs.find.

**6. Tool_use/Tool_Result Integrity Fix** [#31547](https://github.com/anomalyco/opencode/pull/31547)
Defensive fix pairing every `tool_use` with matching `tool_result`. Closes session-stuck bug #27594.

**7. Small Models for Explore Subagents** [#24943](https://github.com/anomalyco/opencode/pull/24943)
Scoped small-model fallback for explore agents, reducing cost.

**8. PWA Support** [#31279](https://github.com/anomalyco/opencode/pull/31279)
Adds service worker, update prompt, and offline support for web app.

**9. Reasoning Options Sync** [#31581](https://github.com/anomalyco/opencode/pull/31581)
Normalizes provider-specific reasoning settings (toggle/effort/budget) from models.dev.

**10. Skill Plugin Config Hook Ordering** [#28647](https://github.com/anomalyco/opencode/pull/28647)
Fixes plugin `config()` hooks running after skill discovery, enabling dynamic skill paths.

## Feature Request Trends
- **Sandboxing/security** (#2242, recurring) — Terminal isolation and file access restrictions for agents remain the #1 feature ask.
- **Context awareness in IDEs** (#3472, #22235) — Users want selected code/errors automatically sent to the agent; current implementation unclear or broken.
- **Local model optimizations** (#31433, #26412) — Context window limits, streaming tool calls, and proper custom provider support for Ollama/vLLM/LM Studio.
- **CLI usability** (#27698, #31582, #18425) — Usage stats in CLI, configurable TUI widths, and a `/copy-last` command for easy response sharing.
- **Speech-to-text input** (#31542) — New request for voice-driven interaction, likely for accessibility or hands-free coding.

## Developer Pain Points
- **Provider fragmentation** — Custom OpenAI-compatible providers have at least 3 distinct bugs (options not passed, image attachments broken, streaming tool call failures). Self-hosted users face a degraded experience.
- **Memory/stability** — Memory leaks (#20695) plus "Tool execution aborted" (#18757) and session-stuck bugs (#27594, #31525) create an unreliable experience for long sessions.
- **IDE integration gaps** — Context awareness (#22235) and file list refresh (#31574) break core IDE workflows.
- **Billing communication** — Two refund/complaint issues (#26508, #29182) suggest poor support responsiveness (12+ days no reply). Community frustration visible.
- **New model incompatibility** — Fable 5 on Bedrock (#31560) and Kimi/DeepSeek V4 pro (#31558) broke immediately, indicating insufficient testing against latest model APIs.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-10

## Today's Highlights

Pi v0.79.1 shipped with Claude Fable 5 support across Anthropic and Amazon Bedrock, alongside prompt template argument defaults—a minor release packing significant model flexibility. The community is buzzing about the new Project Trust feature, generating both the most-commented issue (#5514) and a rapid follow-up PR (#5549) to address UX friction. Several critical thinking-mode bugs for Fable and other adaptive-thinking models received hotfix PRs within hours of being reported.

## Releases

**v0.79.1** — [GitHub Release](https://github.com/badlogic/pi-mono/releases/tag/v0.79.1)

- **Claude Fable 5** support on Anthropic and Amazon Bedrock providers, with adaptive thinking and `xhigh` effort level.
- **Prompt template defaults** — Positional arguments now support `${1:-7}` syntax for optional values in `.ptpl` files.

## Hot Issues

1. **[#5514 — Project Trust Feature Feedback](https://github.com/earendil-works/pi/issues/5514)** *(CLOSED, 24 comments)*  
   Author markg85 vents frustration about trust-gating prompts appearing on every folder, across machines. The community agrees: 12 👍 signals broad demand for persistent trust opt-out or parent-folder inheritance. This triggered the rapid PR #5549.

2. **[#4180 — Links not clickable anymore](https://github.com/earendil-works/pi/issues/4180)** *(CLOSED, 13 comments)*  
   Hyperlinks in agent responses (URLs, markdown links) stopped working after a recent update switched terminal modes. A long-standing regression closed only due to a broader refactor—users still want this fixed properly.

3. **[#4984 — Interactive mode crash on transient terminal EPIPE](https://github.com/earendil-works/pi/issues/4984)** *(CLOSED, 13 comments)*  
   `write EPIPE` crashes on `edit` tool calls when the terminal pipe closes mid-stream. Affects users running Pi in non-interactive or piped contexts. Reproduced reliably, fixed in-progress.

4. **[#4877 — Session folder collision](https://github.com/earendil-works/pi/issues/4877)** *(OPEN, 11 comments)*  
   Paths like `/a/b/c/d` and `/a-b/c-d` hash to the same session folder. Minor but surprising—sessions can collide silently. Community wants path-based disambiguation.

5. **[#4185 — Zsh/tmux installation bad colors/contrast](https://github.com/earendil-works/pi/issues/4185)** *(CLOSED, 10 comments)*  
   Fresh npm install yields unreadable terminal colors in tmux. 6 👍 indicates a common onboarding friction point for terminal-heavy users.

6. **[#5363 — Amazon Bedrock Mantle provider for OpenAI-compatible models](https://github.com/earendil-works/pi/issues/5363)** *(OPEN, 7 comments)*  
   Existing Bedrock provider uses Converse API, but Bedrock Mantle models (GPT-5.5/5.4) need OpenAI-compatible endpoints. PR #5509 implements this already—community wants it landed.

7. **[#5464 — Local models 3-5 minute "Working" latency](https://github.com/earendil-works/pi/issues/5464)** *(CLOSED, 7 comments)*  
   Running Ollama models causes multi-minute "Working" delays even on trivial messages. Critical for offline-first users—context window management or polling loop suspected.

8. **[#5350 — Custom tool operations receive host-OS-resolved paths](https://github.com/earendil-works/pi/issues/5350)** *(OPEN, 6 comments)*  
   Windows host running Linux remote file tools via custom operations gets paths resolved to Windows format (`C:\...`). Breaks SSH file workflows—path normalization gap.

9. **[#4841 — Footer ignores `modelOverrides.name`](https://github.com/earendil-works/pi/issues/4841)** *(CLOSED, 5 comments)*  
   Users set custom model display names in `models.json`, but the footer shows raw model IDs. Contradicts documented behavior; a cosmetic but confusing inconsistency.

10. **[#5427 — OpenAI Codex transport issues](https://github.com/earendil-works/pi/issues/5427)** *(CLOSED, 4 comments)*  
    Codex SSE response headers time out after 10 seconds, recurring on every message after first failure. 4 👍 suggests significant Codex user impact—regression in v0.78.1.

## Key PR Progress

1. **[#5567 — fix(ai): mark Claude Fable 5 thinking off unsupported](https://github.com/earendil-works/pi/pull/5567)** *(CLOSED)*  
   Prevents sending `thinking: { type: "disabled" }` to Fable 5, which Anthropic rejects with 400. Consistent with other adaptive-thinking models. Addresses issue #5569.

2. **[#5563/#5564 — feat(ai): add Claude Fable 5 and Mythos 5 models](https://github.com/earendil-works/pi/pull/5563)** *(CLOSED, two parallel PRs)*  
   Full model metadata for both Anthropic and Bedrock providers. Marks models as always-adaptive thinking, disables temperature, preserves signatures on replay.

3. **[#5561 — feat(ai): add Claude Fable 5 to Amazon Bedrock](https://github.com/earendil-works/pi/pull/5561)** *(OPEN)*  
   Enables effort-based adaptive thinking for Bedrock's Fable 5 deployment, using `output_config.effort` instead of legacy `budget_tokens`. Exposes `xhigh` effort level.

4. **[#5562 — fix(tui): separate list items with blank lines in loose lists](https://github.com/earendil-works/pi/pull/5562)** *(OPEN)*  
   Correctly renders Markdown loose lists per CommonMark spec—items separated by blank lines get vertical spacing. A polish fix for TUI rendering fidelity.

5. **[#5560 — fix(coding-agent): parse `:thinking` suffix from custom model IDs](https://github.com/earendil-works/pi/pull/5560)** *(OPEN)*  
   Users can append `:thinking` to custom model IDs (e.g., `my-model:high`). Fixes edge case where suffix breaks model resolution. Closes #5552.

6. **[#5509 — feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/5509)** *(OPEN)*  
   Entirely new provider for Bedrock Mantle's OpenAI-compatible API. Supports GPT-5.5 and GPT-5.4. Modelled after Azure OpenAI provider—major cloud expansion.

7. **[#5555 — fix(ai): attach reasoning_details streamed before tool_calls](https://github.com/earendil-works/pi/pull/5555)** *(CLOSED)*  
   Encrypted reasoning signatures arriving before tool call chunks (e.g., OpenRouter+Gemini) were silently dropped. Fixes signature loss in interleaved streaming.

8. **[#5549 — feat(ui): Improved project approval settings](https://github.com/earendil-works/pi/pull/5549)** *(CLOSED)*  
   Direct response to #5514: adds global enable/disable flag, parent-folder trust inheritance, and "trust parent" option in approval dialogs. Aligns project trust with VS Code pattern.

9. **[#5553 — Add prompt template argument defaults](https://github.com/earendil-works/pi/pull/5553)** *(CLOSED)*  
   Syntax `$ {1:-7}` for optional positional defaults in `.ptpl` files. Single-pass substitution (no recursive expansion). Documented with regression tests.

10. **[#5547 — feat(coding-agent): add experimental feature guard](https://github.com/earendil-works/pi/pull/5547)** *(CLOSED)*  
    Implements RFC 0043: `PI_EXPERIMENTAL=1` environment variable gates experimental features. Enables safer rollout of risky changes.

## Feature Request Trends

- **Amazon Bedrock Expansion** — Multiple requests and PRs (Mantle provider, inference profile region extraction, Fable 5 deep integration) show AWS is a top-tier provider target.
- **Trust & Permission UX** — The Project Trust firestorm (#5514, #5549, #5523) reveals strong demand for granular, persistent, and inheritable trust settings—users find current prompts disruptive.
- **In-Session Configuration** — `/update` TUI command (#4714), session-only model/thinking changes (#5270), and `/about` startup-info command (#5548) suggest users want richer runtime UI control without restarting.
- **Themed First-Run Experience** — Terminal theme auto-detection (dark/light) in #5385 and consistent CJK text wrapping (#5326, #5283) indicate focus on out-of-box polish for international users.
- **Custom Provider Flexibility** — Custom model ID suffix parsing (#5560), `modelOverrides` respect (#4841), and cost inheritance fixes (#5544) show growing use of self-hosted/edge-case model configurations.

## Developer Pain Points

| Pain Point | Frequency | Key Issues |
|---|---|---|
| **Thinking mode incompatibility** with new adaptive-thinking models | Very High | #5511, #5531, #5541, #5569, PRs #5554, #5567 |
| **Terminal/rendering regressions** — CJK wrapping, kitty keyboard, viewport lock, loose list rendering | High | #5326, #3967, #5192, #4185, PR #5562 |
| **Provider-specific bugs** — Azure context sizes wrong, Codex SSE timeout, Bedrock region parsing, OpenRouter reasoning signatures | High | #5559, #5427, #5270, #5555 |
| **Session/state handling** — folder collisions, usage field crashes, session stats errors | Medium | #4877, #5386, #5337 |
| **Windows/Linux path normalization** — SSH tools, custom operation paths | Medium | #5350, #5192 |
| **Plugin/extension API gaps** — trust state not exposed for MCP extensions, OAuth prompt mirroring | Low | #5523, #5433 |

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-10

## Today's Highlights
Two releases hit the **v0.18.0-preview** channel today, signaling the team's push toward the next major milestone. A CI pipeline failure on both nightly and preview builds (#4912, #4913) will need quick attention. Meanwhile, the community is buzzing around **MCP security** (project-scoped `.mcp.json` with approval gates), **subagent tool fidelity**, and strong demand for **cross-session `/rewind`** and **Dynamic Workflows** inspired by Claude Code's latest features.

## Releases
- **v0.18.0-preview.0** and **v0.18.0-preview.1** — both published within the last 24 hours. The only listed change is `fix(cli): skip thought parts in copy output` by @he-yufeng, plus the automatic `chore(release): v0.17.1`. No detailed release notes beyond that; the preview tag suggests a stabilization phase before v0.18.0 final.
- ⚠️ **Release pipeline failures**: Issue #4913 (v0.17.1-preview.0) and #4912 (nightly) both failed on 2026-06-10. See [failure run](https://github.com/QwenLM/qwen-code/actions/runs/27244745901) and [nightly run](https://github.com/QwenLM/qwen-code/actions/runs/27244604723).

## Hot Issues (Top 10)

1. **#4514 — Daemon capability gaps for `qwen serve`** (14 comments)  
   *Author: doudouOUC*  
   Tracks the remaining gaps in the HTTP/SSE surface after slash-command passthrough. ACP compatibility is converging, but the backlog of edge cases in long-running daemon mode is actively discussed.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4514)

2. **#4782 — ACP Streamable HTTP transport implementation status** (4 comments)  
   *Author: chiga0*  
   Qwen-Code Daemon now implements Streamable HTTP at `/acp`, enabling zero-adapter connections from Zed, Goose, and JetBrains. The community is validating the upgrade path from earlier SSE-based ACP.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4782)

3. **#4615 — Project-scoped `.mcp.json` with pending approval semantics** (5 comments)  
   *Author: qqqys*  
   Proposes a security-first MCP server config — servers shown as `Pending` before any connection starts. This addresses a major trust concern in multi-developer workspaces.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4615)

4. **#4898 — Better control over user profile & auto-skill extraction** (3 comments)  
   *Author: wunan067830-west*  
   Requests more granular control over user profiling and automatic skill extraction to prevent context pollution. High-priority memory management concern.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4898)

5. **#4888 — `ask_user_question` in IDEA plugin not showing question text** (3 comments)  
   *Author: byx1728*  
   IDE integration regression: question text and input fields are missing in IntelliJ, showing only Submit/Cancel buttons. Critical for IDE users.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4888)

6. **#4876 — Subagent reads images but returns unrelated content** (3 comments)  
   *Author: MachineXu*  
   Subagent fails to correctly process image files when using `read_file`, while the main agent handles the same task correctly. Points to subagent context routing bugs.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4876)

7. **#4907 — Down arrow requires 2 presses to reach subagent content** (2 comments)  
   *Author: pomelo-nwu*  
   TUI keyboard navigation glitch: the focus chain skips the live agent tab bar, costing an extra keypress. Lowers UX for multi-agent workflows.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4907)

8. **#4904 — Can't switch to new models (e.g., Qwen3.7-plus)** (2 comments)  
   *Author: Cities2000*  
   Model-switching from Coding Plan integration fails: `qwen3.7-plus` is not offered for the `openai` auth type, even though it's available in the provider. ModelProvider configuration confusion.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4904)

9. **#4882 — Add `terminalSequence` field on hooks** (2 comments)  
   *Author: xibaisike*  
   Following Claude Code v2.1.141, requests a hook field for terminal-side effects (desktop notifications, window-title updates) without a controlling terminal.  
   [GitHub](https://github.com/QwenLM/qwen-code/issues/4882)

10. **#4910 — Support installing extensions from archive files and URLs** (1 comment)  
    *Author: kkhomej33-netizen*  
    Extends the extension installer to accept `.zip`, `.tar.gz`, and direct URLs, complementing existing git/npm/marketplace sources.  
    [GitHub](https://github.com/QwenLM/qwen-code/issues/4910)

## Key PR Progress (Top 10)

1. **#4914 — Harden OOM prevention: idempotent compaction tests, explicit GC**  
   *Author: zzhenyao*  
   Adds regression tests for `compactOldItems` idempotency (follow-up to #4824) and introduces explicit garbage collection in memory-pressure paths. Closes #4815.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4914)

2. **#4897 — Persist file history snapshots for cross-session `/rewind`**  
   *Author: doudouOUC*  
   FileHistorySnapshot is now persisted to JSONL, enabling `/rewind` across session resume (T2.1 graduation). Previously in-memory only, lost on exit.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4897)

3. **#4890 — Add `/cd` command to change working directory without restart**  
   *Author: qqqys*  
   Interactive `/cd` moves the session working directory mid-session, validates paths, prompts for trust, and migrates workspace roots.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4890)

4. **#4844 — Agent Team: experimental parallel sub-agent coordination**  
   *Author: tanzhenxin*  
   Adds experimental Agent Team mode — named teams with parallel sub-agents that message each other, share task lists, and consolidate results via a leader.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4844)

5. **#4732 — Workflow tool P1: `node:vm` sandbox + sequential `agent()`**  
   *Author: LaZzyMan*  
   Implements the first tier of Dynamic Workflows (port from Claude Code 2.1.160). Model-authored JS scripts in a sandboxed VM with `agent()` calls.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4732)

6. **#4896 — Stabilize prompt-cache prefix against MCP/skills churn**  
   *Author: callmeYe*  
   Decouples skill visibility from validation to prevent mid-session skill/MCP changes from invalidating the entire prompt cache. Cache-optimized tier separation.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4896)

7. **#4853 — `enter_plan_mode` tool and Plan Approval Gate**  
   *Author: callmeYe*  
   The model can proactively enter plan mode for complex tasks. In AUTO/YOLO modes, `exit_plan_mode` triggers a single user approval step before execution.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4853)

8. **#4850 — Interactive multi-tab `/extensions` manager**  
   *Author: BZ-D*  
   Upgrades `/extensions` from a flat list to a three-tab interactive UI: Installed, Discover, Sources — covering the full extension lifecycle.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4850)

9. **#4835 — Project-level extension install and management**  
   *Author: BZ-D*  
   Extensions can now be scoped to a project (`project` level in addition to `user`), enabling workspace-specific toolchains.  
   [GitHub](https://github.com/QwenLM/qwen-code/pull/4835)

10. **#4161 — `/auto-improve` command for local repository improvements**  
    *Author: DragonnZhang*  
    Adds a session-scoped loop for small, locally verifiable improvements: source config, start/status/stop controls, scheduled ticks, and local state tracking.  
    [GitHub](https://github.com/QwenLM/qwen-code/pull/4161)

## Feature Request Trends

- **MCP Security & Governance**: Strong demand for project-scoped `.mcp.json` with explicit approval states (#4615), credential management, and scoped extension installs (#4835).
- **Agent & Workflow Orchestration**: Enthusiasm for multi-agent coordination — Agent Teams (#4844), Dynamic Workflows (#4732, #4721), `/cd` for workspace mobility (#4890), and persistent background sessions (#4884).
- **Cross-Session Persistence**: `FileHistorySnapshot` to JSONL (#4897) and memory/mirroring improvements (#4747, #4898) show growing need for state that survives restarts.
- **IDE & UI Integration**: `ask_user_question` in IDEA (#4888), sidebar file panels (#4885), and terminal resize handling (#4891) reflect maturing desktop expectations.
- **Observability & Diagnostics**: Timing metrics (TPS, TTFT) in `/stats` (#4252), `--safe-mode` (#4883), and `terminalSequence` hooks (#4882) indicate demand for deeper instrumentation.

## Developer Pain Points

- **Subagent reliability**: Inconsistent image/file handling in subagents vs. main agent (#4876) erodes user trust in multi-agent setups.
- **Model switching fragility**: Runtime prefix leaks into `settings.model.name` (#4729) and restrictions on provider-agnostic model switching (#4904) cause frequent "model does not exist" errors.
- **Dual Output / JSON-file mode unresponsiveness**: TUI hangs in Dual Output mode (#4727) — a critical failure for headless/automation workflows.
- **Background auto-update corruption**: Mid-session background updates can replace chunks and break cross-authType model switching (#4758).
- **Focus and keyboard navigation**: Subagent content unreachable with a single down-arrow (#4907) and cursor stalling at wrapped-line boundaries (#4852) degrade terminal UX.
- **Windows installation gaps**: `qwen not found` in new sessions after SYSTEM-user installation (#4901) and path normalization issues in CI (#4915) isolate Windows developers.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-10

## Today's Highlights

CodeWhale v0.8.55 shipped with **Together AI**, **OpenAI Codex**, and a new **Model Catalog**, but the rebrand from `deepseek-tui` to `codewhale` is causing upgrade friction. The community is heavily focused on **token efficiency** and **prompt discipline**, with a coordinated push to match Codex CLI's input/output token usage. A new **hippocampal memory system** proposal aims to solve infinite-context and cross-session recall.

## Releases

- **v0.8.55** — New providers: Together AI, OpenAI Codex. Added Model Catalog. **Breaking**: Legacy npm package `deepseek-tui` deprecated; users must migrate per `docs/REBRAND.md`. Canonical name is now `codewhale`.

## Hot Issues

1. **#2942** — [Bug] CodeWhale spontaneously executes unrequested actions, breaking projects  
   *Why it matters:* Core reliability issue — agent hallucinates instructions, causing destructive changes  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2942)

2. **#2922** — [Question] Agent repeatedly announces "YOLO mode" before every atomic operation  
   *Why it matters:* 4 comments show community frustration with verbosity; fix already landed in PR #2933  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2922)

3. **#1990** — [Enhancement] Remote workbench: US-first Cloudflare/AWS/Telegram lane  
   *Why it matters:* High strategic priority — enables global users outside Tencent ecosystem; 3 comments from maintainer  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1990)

4. **#2931** — [Closed] Feature: auto-detect version updates and notify  
   *Why it matters:* Closes a major UX gap — users on old builds won't miss critical fixes; 3 comments  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2931)

5. **#2935** — [Bug] Design: hippocampal memory system for infinite-context and cross-session recall  
   *Why it matters:* Proposes a long-needed architecture for persistent memory beyond 1M-token window  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2935)

6. **#889** — [Enhancement] Accept ACP protocol to adapt to Paseo  
   *Why it matters:* 2 👍 — strong interest in remote task submission via third-party tools  
   [Link](https://github.com/Hmbown/CodeWhale/issues/889)

7. **#2969** — [Bug] CHANGELOG missing v0.8.55 entry  
   *Why it matters:* Documentation hygiene; community caught the gap immediately  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2969)

8. **#2924** — [Bug] npm update path broken for legacy users  
   *Why it matters:* Directly blocks adoption — 1 👍, high-impact for package-manager users  
   [Link](https://github.com/Hmbown/CodeWhale/issues/2924)

9. **#1846** — [Enhancement] Cannot see proposed changes before approving them  
   *Why it matters:* UX blocker for approval workflow — 1 👍, core interaction pattern  
   [Link](https://github.com/Hmbown/CodeWhale/issues/1846)

10. **#2656** — [Bug] Sub-agent session name conflicts hard to diagnose  
    *Why it matters:* Affects multi-agent orchestration reliability; reported by maintainer  
    [Link](https://github.com/Hmbown/CodeWhale/issues/2656)

## Key PR Progress

1. **#2905** — Fix: name `allow_shell` blocker for shell tools  
   *Improves diagnostic clarity when shell execution is disabled; includes regression tests*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2905)

2. **#2947** — Fix: guide long shell work to background  
   *Teaches model to background shell tasks exceeding 5 seconds; addresses #2939*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2947)

3. **#2951** — Fix: explain `visibility="internal"` in Runtime Policy Reference  
   *Adds clarity to system prompt internals for agent understanding*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2951)

4. **#2949** — Refactor: decouple `allow_shell` from static system-prompt prefix  
   *Moves config into per-turn runtime tag for better prefix caching*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2949)

5. **#2946** — Fix: update Bocha web search response handling  
   *Adapts to Bocha API changes with backward-compatible fallback*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2946)

6. **#2945** — Feat: render hotbar in sidebar  
   *UI improvement for keyboard shortcut discovery; part of #2065*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2945)

7. **#2943** — Fix: normalize macOS Cmd to Ctrl for keyboard shortcuts  
   *Solves macOS terminal inconsistency; addresses #2938*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2943)

8. **#2925** — Feat: add dedicated Together AI provider support  
   *Full provider integration — config, CLI, TUI, model registry*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2925)

9. **#2927** — Feat: add Qwen 3.7 Max to OpenRouter model catalog  
   *Expands model choice with correct alias resolution*  
   [Link](https://github.com/Hmbown/CodeWhale/pull/2927)

10. **#2933** — Feat: hippocampal memory system + YOLO mode cleanup + improved error messages  
    *Bundles four fixes: memory system, verbosity reduction, tool/subagent error clarity*  
    [Link](https://github.com/Hmbown/CodeWhale/pull/2933)

## Feature Request Trends

- **Memory & Context**: Strong demand for infinite-context and cross-session recall (hippocampal memory system, #2935). `/compact` and `note` tools seen as insufficient.
- **Remote Workbench**: Urgent push for US-friendly infrastructure (DigitalOcean, AWS, Telegram bridge) to replace Tencent-only path (#1990, #2964, #2965).
- **Token Discipline**: Entire family of issues (#2952–#2962) targeting Codex-parity in token usage — prompt slimming, telemetry normalization, benchmark harness.
- **UI/UX Polish**: Sidebar sessions panel (#2934), hotbar rendering (#2945), macOS keyboard normalization (#2943), change preview before approval (#1846).
- **Multi-Provider Support**: Together AI (#2925), Qwen 3.7 Max (#2927), DeepSeek V4 via Anthropic API (#2963).

## Developer Pain Points

- **Agent Hallucination**: CodeWhale spontaneously executing unrequested operations (#2942) — top community concern, breaks projects.
- **Upgrade Migration Pitfalls**: Rebrand from `deepseek-tui` to `codewhale` causing npm and Cargo update failures (#2924, #2960); CHANGELOG gaps (#2969).
- **Verbose Agent Output**: Repeated mode announcements (#2922) and lengthy status narration (#2959) waste tokens and annoy users.
- **Poor Diagnostic Messages**: Agents cannot easily tell why tools are unavailable (#2657); sub-agent session name conflicts are opaque (#2656).
- **Telegram Bridge Instability**: Approval deadlocks due to serial update dispatch (#2966); missing streaming, resilience, and backoff (#2967).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*