# AI CLI Tools Community Digest 2026-07-06

> Generated: 2026-07-06 01:53 UTC | Tools covered: 9

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
**Date: 2026-07-06**

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape shows a maturing yet fragmented ecosystem with **seven major tools** actively competing for developer mindshare. While Claude Code and OpenAI Codex remain the most heavily discussed (50+ open issues each), newer entrants like **Qwen Code** and **Gemini CLI** are rapidly closing the gap with aggressive feature velocity. A clear divide is emerging between **tool-assisted coding** (Claude Code, Codex, Copilot CLI) and **agentic workflow orchestration** (Gemini CLI, CodeWhale, OpenCode), with the latter category seeing the most architectural innovation around sub-agent management and session lifecycle control. The **Kimi Code CLI** community stands out as an outlier—its most pressing issue is not a technical bug but an incomplete branding migration, signaling organizational growing pains. Across all tools, **safety classifier overreach**, **permission model inconsistency**, and **memory/resource leaks** are universal pain points eroding developer trust.

---

## 2. Activity Comparison (2026-07-06)

| Tool | Open Issues (24h) | PRs Active | Releases Today | Community Engagement Signal |
|------|------------------|------------|----------------|----------------------------|
| **Claude Code** | ~50 | 2 (low) | None | Highest upvote density; 361 👍 on single bug (#73125) |
| **OpenAI Codex** | ~50 | 10 (8 merged) | None | 690 👍 on Linux desktop request; PR-heavy day |
| **Gemini CLI** | ~10 (active today) | 10 (8 automated deps) | Nightly build | P1 bugs in subagent reliability; heavy dependency refresh |
| **Copilot CLI** | 16 updated | 1 (open) | None | Critical hook stdin bug (#4034); low PR throughput |
| **Kimi Code CLI** | 1 updated | 10 pending (from past week) | None | Branding migration tracking closed; zero code changes today |
| **OpenCode** | ~10 (active today) | 10+ | None | Post-outage recovery; high comment count on outage issues |
| **Pi** | 30+ (Jul 5 burst) | 10 (foundational) | None (v0.80.3 stable) | Exceptional burst; mitsuhiko PRs on tool reliability |
| **Qwen Code** | ~10 | 10 | Nightly build | Heavy on daemon performance and session management |
| **CodeWhale** | ~10 | 10 | None | Pre-v0.8.68 ramp-up; WhaleFlow orchestration focus |

**Key observation**: OpenAI Codex and Pi had the most impactful PRs today (8 merged). Gemini CLI and Qwen Code show automated dependency hygiene. Claude Code and Copilot CLI have concerningly low PR throughput relative to their bug backlogs.

---

## 3. Shared Feature Directions

The following requirements appear across **multiple tool communities**, indicating industry-wide developer expectations:

| Feature Need | Tools Requesting | Specific Ask |
|-------------|-----------------|--------------|
| **Session lifecycle management** | Claude Code (#26904), Gemini CLI (#26522), OpenCode (#27167), Qwen Code (#6346) | Persistent session goals, termination guarantees, artifact retention across restarts |
| **Multi-agent orchestration** | Claude Code (#74598), Gemini CLI (#22323), OpenCode (#17994), CodeWhale (#4010) | Sub-agent supervision, context budget management, verification gates |
| **Custom/private model endpoints** | Copilot CLI (#4003), Pi (#6337, #6327), CodeWhale (#3969), Gemini CLI (#19873) | Local model support, per-sub-agent provider routing, enterprise offline use |
| **Tool reliability / constrained generation** | Pi (#6278, #6306, #6341), Claude Code (#74567), Qwen Code (#6338) | Grammar/JSON-schema-constrained tool calling; reduce LLM hallucination in tool arguments |
| **Memory/context management** | Gemini CLI (#26522), Qwen Code (#4184, #6265), CodeWhale (#4015), Claude Code (#64777) | KV-cache preservation, context budget truncation, memory leak detection |
| **Cost transparency & billing fairness** | OpenAI Codex (#30918), Claude Code (#74598), OpenCode (#35475), Copilot CLI (#4032) | Accurate usage metering, not charging for blocked/trivial actions, model pinning |
| **Mobile/remote control** | OpenAI Codex (#9224, 405👍), Claude Code (implied), Copilot CLI (#4011) | Headless/server mode, phone-to-CLI control via ChatGPT app |
| **Permission model consistency** | Claude Code (#74567, #74080), Copilot CLI (#4033), Gemini CLI (#22672) | Auto-approve honoring allowlists, parent-turn intent preservation, destructive action guardrails |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi | Qwen Code | CodeWhale |
|-----------|------------|-------------|------------|-------------|----------|-----|-----------|-----------|
| **Primary user** | Power users, sysadmins, security pros | Pro users, enterprise teams | Google ecosystem devs | GitHub ecosystem devs | Open-source multi-model devs | Tool-chain builders | Chinese-market devs | Workflow engineers |
| **Core strength** | Safety/classifier system (despite overreach) | Plugin/MCP ecosystem breadth | Agentic reasoning depth | GitHub integration seamlessness | Model routing flexibility | Provider diversity & tool reliability | Daemon performance & caching | Agent orchestration (WhaleFlow) |
| **Technical approach** | Skill-forking, subagent model pinning | Plugin discovery, exec-policy management | AST-aware code navigation, agent profiles | Hook-based extensibility, tgrep indexer | Multi-provider routing, session goals | Constrained sampling, smart routing | KV-cache proxy-tool, session profiling | Work graphs, conductor agents |
| **Pain point** | Safety false positives blocking legitimate work | Rate-limiting bugs and Windows stability | Subagent reliability and terminal glitches | Model availability mismatches, OOM crashes | Infrastructure outages, false positive billing | Null content crashes, session integrity | CI bot aggressiveness, startup noise | Dead code accumulation, TUI lag under load |
| **Platform maturity** | Mature but regression-prone | High PR velocity, Windows gaps | Rapid iteration, dependency heavy | Low PR throughput, stable | Post-outage recovery | Foundational refactoring | Feature-rich, China-focused | Pre-release orchestration focus |

**Strategic insight**: Claude Code and Copilot CLI are **maturing but defensive**—their communities are vocal about regressions. OpenAI Codex and Pi are **investing deeply in infrastructure** (plugin system, constrained generation). Gemini CLI, Qwen Code, and CodeWhale are **aggressively innovating** in agent orchestration and session management, areas where incumbents are weakest.

---

## 5. Community Momentum & Maturity

| Tool | Momentum Signal | Maturity Assessment |
|------|----------------|---------------------|
| **Claude Code** | 🟡 **High engagement, low PR velocity** — Community is loud but fixes are slow. 361👍 on a closed bug suggests frustration with resolution pace. | **Mature product, stagnant dev cycle.** 50 open issues with only 2 PRs suggests maintainers are stretched or prioritizing elsewhere. |
| **OpenAI Codex** | 🟢 **Highest PR throughput today** — 8 merged PRs from OpenAI engineers. Strong investment in plugin system and terminal UX. | **Enterprise-grade velocity.** Rate-limiting bugs (#30918) and Windows stability (#31035) are the main chinks in an otherwise solid armor. |
| **Gemini CLI** | 🟢 **Rapid dependency refresh + architectural PRs** — 8 automated bumps + 15-turn cap PR. P1 bugs being tracked aggressively. | **Young, fast-moving.** Subagent infrastructure has known reliability gaps (#22323, #21409), but the team is responsive. |
| **Copilot CLI** | 🔴 **Lowest energy** — 1 PR open, critical hook bug (#4034) has 1 comment. Community feels stagnant relative to peers. | **Mature but neglected.** Model availability mismatches (#3997) and enterprise billing bugs (#4005) suggest maintenance-mode risk. |
| **Kimi Code CLI** | 🔴 **No code changes today** — Branding migration is the only narrative. PRs from past week are pending review. | **Organizational stall.** The "half-done" migration (#2483) and 10+ unresolved naming issues indicate prioritization chaos. |
| **OpenCode** | 🟡 **Recovering from outage** — High comment activity but closed issues suggest fixes are shipping. DeepSeek V4 Flash still broken (#35486). | **Resilient community.** 104👍 on /goal feature (#27167) shows strong power-user demand. Plugin system needs hardening. |
| **Pi** | 🟢 **Exceptional burst** — 30+ issues, 10 PRs, mitsuhiko (Armin Ronacher) landed foundational fixes. New providers added. | **Renewed energy.** The constrained sampling PR (#6341) and null-content fix (#6343) address the two most painful bugs. This project is accelerating. |
| **Qwen Code** | 🟢 **Heavy feature investment** — Session profiling, artifact retention, scheduled tasks, WeCom channel. | **Rapidly maturing.** Daemon performance focus (#6312) and KV-cache fix (#6268) show architectural depth. CI bot UX (#6299) needs attention. |
| **CodeWhale** | 🟡 **Pre-release ramp-up** — WhaleFlow v0.8.68 is the sole focus. TUI performance under load (#4014) is a real concern. | **Early stage, high ambition.** The orchestration vision is compelling, but the TUI lag and agent reliability bugs need to be solved before GA. |

**Momentum ranking**: Pi > OpenAI Codex > Qwen Code > Gemini CLI > OpenCode > CodeWhale > Claude Code > Copilot CLI > Kimi Code CLI

---

## 6. Trend Signals

### 🚀 Industry Trends from Community Feedback

1. **From "chat copilot" to "agent orchestrator"** — The most active innovation is in **multi-agent workflow orchestration** (CodeWhale WhaleFlow, Gemini CLI subagents, OpenCode multi-agent). Developers no longer want a single assistant—they want a **team of agents** with supervisors, context budgets, and verification gates.

2. **Tool reliability is the new frontier** — Pi's constrained sampling PR (#6341) and Qwen Code's KV-cache proxy-tool (#6268) signal that **LLM hallucination in tool arguments** is now recognized as a critical failure mode. The industry is moving from "does the tool exist?" to "does the tool execute correctly 99.9% of the time?"

3. **Safety systems are breaking trust** — Across Claude Code (false positives on security work), OpenCode (charged ~$20 for blocked content), and Gemini CLI (destructive `git reset`), the **safety-classifier vs. user-intent conflict** is the most painful cross-tool pain point. Expect a backlash if these systems don't become more transparent and configurable.

4. **Enterprise demands are driving feature requirements** — Custom model endpoints (Copilot CLI #4003), business access tokens (Codex #25246), enterprise billing entity selection (Copilot CLI #4005), and telemetry buffering (Gemini CLI PR #28162) all point to **enterprise adoption as a forcing function** for tool maturity.

5. **Windows remains a second-class platform** — OpenAI Codex has 4 distinct Windows-critical bugs. Claude Code has UTF-8 surrogate crashes affecting Windows. Copilot CLI can't uninstall on Windows 11 (#3662). **Windows developers face a consistently worse experience** across the ecosystem.

6. **Memory leaks are systemic** — Every major tool has a class of memory/resource leak:
   - Claude Code: Headless sessions never terminate (#74633)
   - Codex: MCP server processes never cleaned up (#30408)
   - Copilot CLI: `tgrep` indexer OOM-kills hosts (#3976)
   - CodeWhale: TUI memory pressure with 30+ agents (#4014)
   - Qwen Code: Large tool results cause OOM (#4184)
   
   This is a **cross-cutting infrastructure debt** that will become a competitive differentiator.

7. **China-market providers are gaining traction** — Doubao (Pi PR #6327), StepFun (Pi PR #6337), WeCom (Qwen Code PR #6224), and LongCat/Meituan (CodeWhale PR #4034) indicate **ecosystem fragmentation along geopolitical lines**. Tools that support Chinese providers will win the Chinese developer market.

### 💡 Actionable Recommendations for Developers

| If You Need... | Recommended Tool(s) | Rationale |
|---------------|---------------------|-----------|
| Reliable tool execution | **Pi** (constrained sampling incoming) | Armin Ronacher's PRs directly address #1 pain point |
| Multi-agent workflows | **CodeWhale** or **Gemini CLI** | Most advanced orchestration visions |
| GitHub ecosystem integration | **Copilot CLI** | Despite low velocity, GitHub integration is seamless |
| Enterprise deployment | **OpenAI Codex** | Best PR velocity, plugin system, and enterprise auth work |
| Cost-sensitive / multi-model | **OpenCode** or **Pi** | Best model routing flexibility and provider diversity |
| Chinese developer ecosystem | **Qwen Code** | Native WeCom, DingTalk, QQ Bot support |
| Stable, mature tool | **Claude Code** | Most battle-tested, despite regression pain points |

**Final verdict**: The AI CLI tools ecosystem is in a **Cambrian explosion phase** for agent orchestration, a **consolidation phase** for tool reliability, and a **backlash phase** against safety overreach. The tools that ship **constrained tool execution, transparent billing, and robust session management** in the next 6 months will emerge as the long-term winners.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the anthropics/skills repository.

---

## Claude Code Skills Community Highlights Report (Data as of 2026-07-06)

### 1. Top Skills Ranking (Most-Discussed Pull Requests)

The following Pull Requests represent the most active Skill development conversations, ranked by community engagement.

1.  **#1298: fix(skill-creator): run_eval.py always reports 0% recall** (Open)
    - **Functionality:** A critical fix for the `skill-creator` toolchain. Patches `run_eval.py` so the description-optimization loop (`run_loop.py`) evaluates skills accurately instead of always getting 0% recall.
    - **Discussion:** Resolves a major blocker for skill authors, cross-referencing Issue #556 (which has 12 comments and 7 👍). Focuses on Windows subprocess handling, artifact installation, and trigger detection.
    - **Status:** Open
    - **Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

2.  **#514: Add document-typography skill** (Open)
    - **Functionality:** A quality-of-life skill for document generation. Prevents common typographic errors in AI-generated content: orphan word wrap, widow paragraph headers, and numbering misalignment.
    - **Discussion:** Community interest is high because these issues affect nearly every Claude-generated document. The skill addresses a universally-felt pain point in output polish.
    - **Status:** Open
    - **Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

3.  **#83: Add skill-quality-analyzer and skill-security-analyzer** (Open)
    - **Functionality:** Two "meta-skills" for auditing other Skills. `skill-quality-analyzer` scores across Structure, Best Practices, and Performance; `skill-security-analyzer` flags prompt injection, data exfiltration, and privilege escalation risks.
    - **Discussion:** Proposes a structured quality gate for the ecosystem. The security analyzer directly addresses the trust boundary concerns raised in Issue #492.
    - **Status:** Open
    - **Link:** [PR #83](https://github.com/anthropics/skills/pull/83)

4.  **#1367: feat(skills): add self-audit** (Open)
    - **Functionality:** A universal output auditing skill. Performs mechanical file verification (Step 0) followed by a four-dimension reasoning audit (Correctness, Completeness, Consistency, Clarity) in damage-severity priority order.
    - **Discussion:** Proposes a "before-delivery" quality gate for any model or project. The concept of a universal, priority-ordered audit has generated significant discussion.
    - **Status:** Open
    - **Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367)

5.  **#723: feat: add testing-patterns skill** (Open)
    - **Functionality:** Comprehensive skill covering the full testing stack: philosophy (Testing Trophy), unit testing (AAA pattern), React component testing, integration, and mocking.
    - **Discussion:** Addresses a demand for consolidated, best-practice testing guidance within a single Claude session, covering "what to test vs. what NOT to test."
    - **Status:** Open
    - **Link:** [PR #723](https://github.com/anthropics/skills/pull/723)

6.  **#486: Add ODT skill** (Open)
    - **Functionality:** Enables Claude to create, fill, read, and convert OpenDocument Format files (.odt, .ods), a requirement for LibreOffice and enterprise environments.
    - **Discussion:** Fills a gap in document format support. The PR includes triggers for "ODT," "ODS," and "OpenDocument," signaling strong enterprise use-case interest.
    - **Status:** Open
    - **Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

7.  **#806: feat: add sensory skill — native macOS automation via AppleScript** (Open)
    - **Functionality:** Teaches Claude to use `osascript` for native macOS automation (e.g., app scripting, UI manipulation) instead of screenshot-based computer use, with a tiered permission system.
    - **Discussion:** Proposes a more efficient and reliable alternative to vision-based desktop automation, specifically for macOS users.
    - **Status:** Open
    - **Link:** [PR #806](https://github.com/anthropics/skills/pull/806)

---

### 2. Community Demand Trends (From Issues)

The most-anticipated new Skill directions, as indicated by Issue activity:

- **Agent Safety & Governance (High Demand):** Issue #492 (34 comments, highest on record) highlights a critical trust boundary vulnerability: community skills distributed under `anthropic/` impersonate official ones. This has spurred demand for dedicated **skill security and provenance verification** tools.
- **Enterprise Document Automation:** Issue #1175 discusses security and context window management for handling SharePoint Online documents. Combined with the ODT (#486) and DOCX fixes (#541), there is a clear push toward **secure, enterprise-grade document workflows**.
- **Team/Org Skill Sharing:** Issue #228 (14 comments) requests an **org-wide skill library** to replace the current manual file-sharing process. The community wants a shared repository or direct linking mechanism for Claude.ai.
- **Cross-Platform Compatibility:** Issues #1061 and #556 highlight significant **Windows compatibility blockers** in the `skill-creator` toolchain. This is the most technically urgent demand, as a portion of the community is currently locked out of skill development.
- **Symbolic Memory & Context Management:** Issue #1329 proposes a "compact-memory" skill for long-running agents, using symbolic notation to compress agent state and notes, saving context window space.

---

### 3. High-Potential Pending Skills

These PRs are currently open with active discussion, indicating high likelihood of landing soon:

- **#1298 / #1099 / #1050 / #362 (skill-creator fixes):** A cluster of PRs fixing the `skill-creator` toolchain—the most critical infrastructure problem in the repository. All address the 0% recall bug on Windows. These are likely to be consolidated into a single merge.
- **#1367 (self-audit skill):** Near-complete proposal with a clear v1.3.0 versioning. Its universal applicability (any project, any model) and structured approach make it a strong candidate for inclusion.
- **#1302 (color-expert skill):** A mature, well-scoped skill covering comprehensive color expertise (naming systems, spaces, palettes). Low controversy, high utility for design-adjacent workflows.

---

### 4. Skills Ecosystem Insight

**Most concentrated demand:** The community's top priority is **foundational toolchain reliability and security**—specifically, fixing the broken `skill-creator` validation loop on Windows and establishing provenance verification to prevent trust boundary abuse, *before* expanding into new domain-specific Skills.

---

# Claude Code Community Digest — 2026-07-06

## Today's Highlights

The Claude Code community remains highly active with **50 open issues** and significant discussion around several critical bugs. The most pressing concern is **Issue #73125**, a closed bug regarding Claude failing to wait for user responses after 60 seconds, which has garnered **125 comments and 361 upvotes** — the highest community engagement this week. Multiple reports of **safety classifier false positives** blocking legitimate security and systems administration work continue to surface, alongside a new wave of bugs related to the **Fable 5 model** including silent turns and billing discrepancies in subagent workflows.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[[BUG] AskUserQuestion: "No response after 60s — continued without an answer"** (#73125 — CLOSED)
   *Impact*: Critical UX bug where Claude Code stops waiting for user input after 60 seconds, continuing without confirmation. 361 👍 reactions and 125 comments indicate widespread frustration. The label mix (bug, api:bedrock, platform:linux, area:tui, area:tools, platform:vscode) suggests this crosses multiple surfaces.
   [Link](https://github.com/anthropics/claude-code/issues/73125)

2. **GitHub connector links successfully but cannot access content** (#71542 — OPEN)
   *Impact*: Account-wide regression where Claude's GitHub connector authenticates but returns empty content for all repositories. 27 comments suggest ongoing investigation. A blocker for anyone relying on GitHub integration.
   [Link](https://github.com/anthropics/claude-code/issues/71542)

3. **False positive usage policy violation on computational biology** (#50892 — CLOSED)
   *Impact*: Closed as duplicate, but with 9 comments and 2 👍, reflects a **recurring theme** of legitimate scientific/security work being blocked. Contributed to the broader classifier-overreach conversation.
   [Link](https://github.com/anthropics/claude-code/issues/50892)

4. **Subagent model pin lost on injected wake/resume turns** (#74598 — OPEN)
   *Impact*: Technical users running multi-agent workflows are surprised by **unexpected billing changes** — subagents pinned to cheaper models silently switch to the waker's (potentially expensive) model after a resume. Has a reproduction case, making this actionable.
   [Link](https://github.com/anthropics/claude-code/issues/74598)

5. **Classifier blocks user-authorized actions inside forked skills** (#74080 — OPEN)
   *Impact*: When forking skills, the classifier loses visibility of parent-turn intents, causing blocks on actions the user already approved. 4 comments, regression-labeled, affecting power users building skill chains.
   [Link](https://github.com/anthropics/claude-code/issues/74080)

6. **`--permission-mode dontAsk` denies Write/Edit regardless of allowedTools** (#74567 — OPEN)
   *Impact*: Headless/CI users trying to automate file edits find `dontAsk` mode unconditionally denies writes, contradicting its documented auto-approve behavior. Blocks agentic workflows. Has reproduction steps.
   [Link](https://github.com/anthropics/claude-code/issues/74567)

7. **API Error 400 — UTF-8 surrogates not allowed** (#64777 — OPEN)
   *Impact*: Duplicate reports (#68737 also open) of mid-conversation crashes due to invalid UTF-8 surrogate pairs in request bodies. Windows and macOS affected. Blocks long sessions with special characters.
   [Link](https://github.com/anthropics/claude-code/issues/64777)

8. **Fable 5 thinking blocks rendered as empty stubs in VS Code** (#66887 — OPEN)
   *Impact*: Fable 5's thinking blocks render as unclickable empty placeholders in the VS Code extension, degrading the model's key UX differentiator. Multiple platforms affected.
   [Link](https://github.com/anthropics/claude-code/issues/66887)

9. **Fable 5 mid-turn text delivered as summarized thinking blocks** (#74558 — OPEN)
   *Impact*: User-facing text intermittently gets routed into "thinking" blocks, making the model appear to skip responses. Has reproduction on Linux/WSL2 and affects transcript-export consumers.
   [Link](https://github.com/anthropics/claude-code/issues/74558)

10. **Safety classifier false positives on defensive security patching** (#74630 — OPEN)
    *Impact*: A sysadmin reports **silent model downgrade** mid-task when performing routine SQL injection fixes and firewall configurations. Multiple duplicates (#74610, #74615) suggest this is actively harming security professionals. Community concern is high.
    [Link](https://github.com/anthropics/claude-code/issues/74630)

## Key PR Progress

*Only 2 PRs updated in the last 24 hours — noteworthy PR activity is low this period.*

1. **toekn** (#66854 — CLOSED)
   *Note*: Title appears to be a typo; likely a trivial or test PR. Closed without merge.
   [Link](https://github.com/anthropics/claude-code/pull/66854)

2. **docs: fix GitHub capitalization in README** (#73476 — OPEN)
   *Detail*: Minor documentation fix correcting "Github" to "GitHub". No functional impact.
   [Link](https://github.com/anthropics/claude-code/pull/73476)

## Feature Request Trends

Based on analysis of all issues opened/updated in the last 24h:

- **Session Management & Deletion**: #26904 ("Add /delete command to delete current session") has 50 👍 and 7 comments, showing strong demand for CLI-native session lifecycle control.
- **Markdown Copy Support**: #74628 requests proper markdown formatting in copy/paste operations — current behavior strips all markdown, which breaks documentation flows.
- **Bang Command Provenance**: #74629 asks for the model to receive context about *how* input arrived (e.g., `!` shell commands vs. typed prompts) to avoid confusion in multi-input sessions.
- **Computer Use Permissions Rethink**: #74631 critiques the per-app `request_access` model, arguing incomplete app recognition pushes users toward riskier standing-permission grants — a design-level feature request, not just a bug.
- **Scheduled Task Cleanup**: #74633 (bug with feature implications) shows headless sessions never terminate, leaking processes and RAM — users want session lifecycle guarantees for CI/CD use.

## Developer Pain Points

Several **recurring frustrations** emerge from this week's issue traffic:

1. **Safety Classifier Overreach** — Multiple reports (electrical: #74630, #74610, #74615; biological: #50892, #64608) of legitimate **cybersecurity hardening, SIEM deployment, and scientific computing** being blocked. The most severe impact is **silent model downgrade** mid-task — where Claude switches to a weaker model without telling the user. This is consistently the most upvoted category of bug.

2. **Inconsistent Permission Models** — `dontAsk` mode (#74567) not honoring allowlists, fork-skills losing parent intent (#74080), and per-app `request_access` gaps (#74631) create a fragmented permission experience where **what the user explicitly authorized is not respected**.

3. **MCP Server Name Collisions** — When two MCP servers share the same binary/name (#74635), *neither* server's tools are exposed. This is a silent failure with no error message, wasting significant debugging time.

4. **Session Leaks in Automation** — Scheduled tasks (#74633) don't terminate, leaking ~48 headless processes per day with GBs of RAM. **Headless/CI users are paying for processes that should have died hours earlier.**

5. **Cross-Platform Input Gaps** — AltGr characters blocked on international keyboards (#72021), UTF-8 surrogate crashes (#64777), and VS Code thinking-block rendering (#66887) indicate **basic input/output compatibility issues** that erode trust across platforms.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest
**Date: 2026-07-06**

---

## Today's Highlights

The Codex community remains highly engaged with 50 open issues updated in the last 24 hours, though no new releases were published. The hottest discussion continues around the long-standing request for a Linux desktop app (143 comments, 690 upvotes), while a newly surfaced bug report about GPT-5.5 reasoning-token clustering at fixed boundaries (516/1034/1552 tokens) has sparked significant debate about potential model performance degradation. On the development side, eight pull requests from OpenAI engineers landed today, primarily focused on improving terminal handling, autocomplete behavior, and exec-policy management.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#11023: Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**
   - **Why it matters:** This is the most upvoted open issue (690 👍) with a staggering 143 comments. Users are frustrated by macOS performance issues and want Linux support for their desktops. Community sentiment is overwhelmingly positive, with many users offering to help test.
   - **Status:** OPEN (created Feb 2026, updated today)

2. **[#30364: GPT-5.5 reasoning-token clustering at 516/1034/1552](https://github.com/openai/codex/issues/30364)**
   - **Why it matters:** A data-driven bug report showing that GPT-5.5 responses disproportionately land at specific reasoning-token counts (516, 1034, 1552). The author correlates this with degraded performance on complex tasks. 189 upvotes indicate broad community concern about model quality.
   - **Status:** OPEN (created June 27, updated today)

3. **[#8648: Codex replies to earlier messages instead of latest](https://github.com/openai/codex/issues/8648)**
   - **Why it matters:** A persistent conversation-session bug where the assistant responds to earlier messages in long threads, breaking multi-turn workflows. Affects Pro users on high-end models.
   - **Status:** OPEN (created Jan 2026, updated yesterday)

4. **[#9224: Codex Remote Control](https://github.com/openai/codex/issues/9224)**
   - **Why it matters:** 405 upvotes for the ability to control Codex CLI from a phone via ChatGPT app. A strong signal that mobile/remote workflows are a major community priority.
   - **Status:** CLOSED (labeled as "Feature" but likely tracked elsewhere)

5. **[#29000: Codex CLI SIGTRAP crash on Intel macOS](https://github.com/openai/codex/issues/29000)**
   - **Why it matters:** A critical stability bug affecting Intel Mac users. Codex CLI 0.141.0 crashes with `SIGTRAP` on Darwin x86_64, rendering the tool unusable for this hardware segment.
   - **Status:** CLOSED (fixed in later versions)

6. **[#28507: "Selected model is at capacity" error](https://github.com/openai/codex/issues/28507)**
   - **Why it matters:** Pro 5x users hitting persistent model-capacity errors. This is a recurring complaint that suggests capacity management issues on OpenAI's side, not just user error.
   - **Status:** OPEN (created June 16)

7. **[#31035: Windows Codex installs SysmonDrv causing BSODs](https://github.com/openai/codex/issues/31035)**
   - **Why it matters:** A serious Windows kernel-level issue where the desktop app reinstalls Sysinternals Sysmon driver (`SysmonDrv.sys`) even after forced uninstall, leading to Blue Screens of Death. High severity but low engagement (0 upvotes) suggests it may be niche.
   - **Status:** OPEN (created July 3)

8. **[#30918: Usage limits draining abnormally fast on Plus](https://github.com/openai/codex/issues/30918)**
   - **Why it matters:** Users report usage jumping from 70% to 100% in ~6 minutes during normal use. Combined with #30939 (5-10x too fast), this indicates a systemic rate-limiting bug that may be overcharging users.
   - **Status:** OPEN (created July 2)

9. **[#18460: Persistent "Unable to transcribe audio"](https://github.com/openai/codex/issues/18460)**
   - **Why it matters:** Voice dictation in the desktop app is unreliable, particularly on macOS ARM. Long-standing issue (April 2026) with no fix yet.
   - **Status:** OPEN (created April 18)

10. **[#25246: Business access-tokens broken (401 unauthorized)](https://github.com/openai/codex/issues/25246)**
    - **Why it matters:** Business-tier users cannot authenticate via access tokens, breaking enterprise workflows. The `developers.openai.com/codex/enterprise/access-tokens` endpoint is non-functional.
    - **Status:** OPEN (tracker, created May 30)

---

## Key PR Progress

1. **[#31188: Preserve managed exec policy after rules parse errors](https://github.com/openai/codex/pull/31188)**
   - **What:** Fixes a fallback bug where malformed `.rules` files would wipe the entire exec policy, dropping managed requirements.
   - **Impact:** Critical for users with custom rules who need security guarantees maintained even when their rule files have errors.

2. **[#31201: Reduce repeated plugin discovery work during tool assembly](https://github.com/openai/codex/pull/31201)**
   - **What:** Caches plugin metadata (30s TTL) and reuses parsed catalog entries when on-disk bytes are unchanged. Avoids stale suggestions from direct edits.
   - **Impact:** Performance improvement for tool assembly, especially in plugin-heavy environments.

3. **[#30982: Allow extension-managed Apps authentication](https://github.com/openai/codex/pull/30982)**
   - **What:** Lets trusted host extensions provide OAuth/auth for the built-in Codex Apps MCP server. Keeps tool/connector caches isolated per ChatGPT auth identity.
   - **Impact:** Enables third-party extensions to integrate with Codex Apps securely.

4. **[#31192: Flush queued terminal input before exit](https://github.com/openai/codex/pull/31192)**
   - **What:** Fixes a bug where key-release events queued after shutdown could leak corrupted CSI-u sequences into the parent shell.
   - **Impact:** Cleaner terminal behavior on exit; prevents "garbage" characters in the shell after Codex closes.

5. **[#31191: Handle completion separators and popup dismissal](https://github.com/openai/codex/pull/31191)**
   - **What:** Fixes autocomplete inserting redundant spaces when a separator already exists, and prevents popup dismissal from suppressing the wrong token.
   - **Impact:** Better autocomplete UX with fewer accidental whitespace errors.

6. **[#30463: Fix autocomplete targeting between mentions](https://github.com/openai/codex/pull/30463)**
   - **What:** When cursor is between an unbound skill mention and a bound one, correctly targets the unbound token for popup completion.
   - **Impact:** Fixes confusing behavior where autocomplete would offer completions for the wrong mention.

7. **[#31190: Use popup token ranges for autocomplete insertion](https://github.com/openai/codex/pull/31190)**
   - **What:** Threads token-range data through autocomplete flow so acceptance doesn't independently recompute boundaries that may disagree.
   - **Impact:** More reliable autocomplete insertion at ambiguous cursor positions.

8. **[#31189: Fix cancelled review leaving MCP startup busy](https://github.com/openai/codex/pull/31189)**
   - **What:** Prevents the TUI from getting stuck in "Starting MCP servers" state after canceling an inline review, which blocked subsequent `/review` commands.
   - **Impact:** Unblocks users who cancel review tasks—no more "hung" CLI state.

9. **[#31182: Emit thread idle after guardian circuit-breaker interrupts](https://github.com/openai/codex/pull/31182)**
   - **What:** Ensures the thread-idle lifecycle runs after a guardian circuit-breaker abort, preventing a "stopped" thread with an active goal.
   - **Impact:** Fixes threads that appear hung after safety/guardian interruptions.

10. **[#31176: Retry goals after model capacity errors](https://github.com/openai/codex/pull/31176)**
    - **What:** Instead of stopping active goals when a turn ends with a model-capacity error, Codex will retry (with backoff to avoid hot loops).
    - **Impact:** Reduces user frustration from "Model at capacity" forcing manual restarts.

---

## Feature Request Trends

The most demanded features from the open issues are:

- **Linux desktop app** (Issue #11023, 690 👍): The single highest-requested feature. Users need a native Linux client to escape macOS performance issues and utilize Linux desktop resources.
- **Remote/mobile control** (Issue #9224, 405 👍): Users want to control Codex CLI running on a desktop from their phone via the ChatGPT app. This suggests a strong desire for headless or server-mode operation.
- **Export chat as markdown** (Issue #17241): A recurring ask for the desktop app equivalent of CLI's `/copy` command.
- **Better session/thread management** (Issues #30385, #27284): Missing threads in sidebar, SSH remote showing "No chats" despite existing data—users want robust session persistence and UI.

---

## Developer Pain Points

Several systemic pain points emerge from this week's activity:

1. **Rate-limiting bugs:** Multiple reports (#30918, #30939, #28507, #19830) show usage burning 5-10x faster than expected. Some users lose 46% of their 5-hour window in one message. This is the most urgent developer-facing issue—it breaks trust in the billing model.

2. **Windows stability problems:** Four distinct Windows-specific issues appeared: Sysmon BSODs (#31035), session viewport jumps in WSL (#22936), automation threads that never start (#19011), and oversized session files crashing the main process (#22004). Windows remains a second-class platform.

3. **GPT-5.5 quality concerns:** Beyond the token-clustering bug (#30364), users are openly complaining about model degradation (#28885: "too stupid to use it now"). Whether real or perceived, the community sentiment around 5.5 is negative.

4. **MCP server process leaks:** Issue #30408 highlights that MCP server processes spawned per-thread are never cleaned up, leading to 9+ GB RSS over time. This is a significant memory leak in a core infrastructure component.

5. **Authentication breakage:** Business-tier access tokens (#25246) are broken, and browser plugin backends fail to register (#26470). Enterprise adoption is directly impacted by these login/auth failures.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-06

## Today's Highlights
A massive dependency refresh landed today with 10+ automated PRs bumping core libraries (including `@google/genai` from v1 to v2, Puppeteer 24→25, ESLint 9→10), alongside continued bugfix focus on subagent termination logic and terminal hang issues. The community is actively discussing a critical P1 bug where subagents falsely report `GOAL` success after hitting their turn limit, masking real interruptions.

## Releases
- **v0.51.0-nightly.20260706.gf7af4e518** — Automated nightly build. No user-facing changelog beyond the increment. [Compare diff](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260705.gf7af4e518...v0.51.0-nightly.20260706.gf7af4e518)

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS falsely reports GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** 🔥 P1 bug. A `codebase_investigator` subagent signals `status: "success"` with `"GOAL"` termination even when it hit the maximum turn limit mid-analysis. This masks real failures. 10 comments, 2 upvotes.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** P1 with 8 upvotes. Users report `gemini-cli` freezing when deferring to the generalist agent for tasks as simple as folder creation. The workaround is disabling subagents entirely — not ideal.

3. **[#25166 — Shell command hangs with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** P1 bug affecting core execution. Simple CLI commands complete but Gemini continues showing them as active. 3 upvotes from frustrated developers.

4. **[#19873 — Leverage model's bash affinity via zero-dependency sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** P2 enhancement discussing how Gemini 3 models natively prefer `grep`/`sed`/`awk`. Proposes sandboxing to unlock this safely. 8 comments, high architectural interest.

5. **[#24353 — Robust component-level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** P1 EPIC tracking the evolution of behavioral eval tests (now 76 tests, 6 Gemini models). Critical for quality assurance as agent capabilities expand.

6. **[#22745 — AST-aware file reads, search, and codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** P2 EPIC exploring whether AST-aware tools (e.g., method-bound reads) can reduce turn count and token waste. Cross-references experimental `tilth`/`glyph` tools.

7. **[#21968 — Gemini doesn't use skills and sub-agents autonomously](https://github.com/google-gemini/gemini-cli/issues/21968)** P2 bug. Users report custom skills (gradle/git) are ignored unless explicitly commanded, defeating the agentic promise.

8. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** P2 bug in the memory system. Sessions not read by the extraction agent remain "unprocessed" and get re-surfaced endlessly, creating noise.

9. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** P2 security concern: sensitive content enters model context before redaction occurs. Also addresses excessive logging of skill transcripts.

10. **[#22672 — Agent should discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** P2 customer-issue. The agent occasionally runs `git reset`/`--force` when safer alternatives exist. Community wants built-in safety guardrails.

## Key PR Progress

1. **[#28298 — Nightly version bump](https://github.com/google-gemini/gemini-cli/pull/28298)** Automated release preparation for v0.51.0-nightly.

2. **[#28295 — Bump @google/genai 1.30.0 → 2.10.0](https://github.com/google-gemini/gemini-cli/pull/28295)** Major version jump for the underlying GenAI SDK, likely bringing new model capabilities and API changes.

3. **[#28294 — Bump @agentclientprotocol/sdk 0.16.1 → 1.0.0](https://github.com/google-gemini/gemini-cli/pull/28294)** First stable release of the Agent Client Protocol SDK. Could enable new MCP interoperability.

4. **[#28292 — Bump puppeteer-core 24 → 25](https://github.com/google-gemini/gemini-cli/pull/28292)** Major browser automation upgrade for the Browser Agent.

5. **[#28288 — Bulk npm dependencies update (74 packages)](https://github.com/google-gemini/gemini-cli/pull/28288)** Large hygiene PR touching `simple-git`, `@octokit/rest`, `vitest` and many more.

6. **[#28293 — Bump ESLint 9 → 10](https://github.com/google-gemini/gemini-cli/pull/28293)** Major linter upgrade with new rules and performance improvements.

7. **[#28290 — Bump chrome-devtools-mcp 0.19.0 → 1.4.0](https://github.com/google-gemini/gemini-cli/pull/28290)** Major jump for Chrome DevTools MCP integration, likely improving debugging capabilities.

8. **[#28164 — Limit recursive reasoning turns per user request](https://github.com/google-gemini/gemini-cli/pull/28164)** Implements a 15-turn cap on recursive agent reasoning to prevent infinite loops, protecting API quotas and CPU resources.

9. **[#28268 — Clean up profile selector logic](https://github.com/google-gemini/gemini-cli/pull/28268)** Removes legacy configuration and simplifies CLI profile management.

10. **[#28162 — Buffer chat compression telemetry](https://github.com/google-gemini/gemini-cli/pull/28162)** Enterprise-focused fix wrapping OTEL log emission in telemetry buffering, fixing issue #23445.

## Feature Request Trends

- **AST-aware code navigation** — Multiple issues (#22745, #22746) propose using abstract syntax trees for precise method/class reads, reducing token waste from line-based tools.
- **Zero-dependency sandboxing** — Interest in running bash commands safely without containers, leveraging models' native `grep`/`sed`/`awk` affinity (#19873).
- **Subagent trajectory transparency** — Requests to expose subagent execution traces via `/chat share` (#22598) and include subagent context in bug reports (#21763).
- **Better self-awareness** — The CLI should accurately describe its own capabilities, hotkeys, and CLI flags to users (#21432).
- **Memory system robustness** — Auto Memory improvements around patch validation, redaction, and avoiding infinite retries (#26522, #26523, #26525).

## Developer Pain Points

1. **Subagent reliability** — Subagents falsely report success on interruption (#22323), hang indefinitely (#21409), don't use custom skills (#21968), and can run without permission after upgrades (#22093).
2. **Terminal/IO glitches** — Shell commands hang post-completion (#25166), terminal corruption on editor exit (#24935), flickering on resize (#21924), and `\n` escape mishandling (#22466).
3. **Tool overload** — 400 errors when >128 tools are enabled (#24246). Agents need smarter tool scoping.
4. **Configuration blind spots** — Symlinked agents aren't recognized (#20079), `settings.json` overrides ignored by Browser Agent (#22267), and `maxSessionTurns` bypassed (#28164 workaround).
5. **Destructive operational behavior** — Models use `git reset --force` unnecessarily (#22672) and scatter temp scripts across the filesystem (#23571), creating cleanup burden.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-06

## Today's Highlights
A critical bug (#4034) regarding hook subprocess stdin handling was reported, where documented patterns like `$(cat)` may hang indefinitely for tool-use hooks. The community continues to surface significant issues around custom model endpoint support (#4003), memory exhaustion from the native `tgrep` indexer (#3976), and enterprise billing configuration breakage (#4005). No new releases were published in the last 24 hours.

## Releases
None in the last 24 hours.

## Hot Issues (10 of 16)

| Issue | Status | Summary | Impact |
|-------|--------|---------|--------|
| [#3997 — Model "gpt-5.3-codex" not available](https://github.com/github/copilot-cli/issues/3997) | Open (Triage) | User cannot run agent because CLI requests an unavailable model. 10 comments. | Blocks core functionality for affected users; model availability mismatch between client config and server. |
| [#3662 — Can't uninstall on Windows 11](https://github.com/github/copilot-cli/issues/3662) | Open (Windows, Installation) | Control Panel uninstall does nothing; user asks for manual command. 3 comments. | Recurring Windows installation management issue, no fix provided. |
| [#4003 — Custom model endpoint support](https://github.com/github/copilot-cli/issues/4003) | Open (Models) | Request to support local/private model endpoints like VS Code. 2 comments. | High demand; would unlock enterprise and offline use cases. |
| [#4034 — Hook subprocess stdin left open (no EOF)](https://github.com/github/copilot-cli/issues/4034) | Open (Triage) | `preToolUse`/`postToolUse` hooks never close stdin, causing documented `$(cat)` pattern to hang. 1 comment. | **Critical bug** — breaks documented hook API for tool-use hooks; hotfix needed. |
| [#4017 — MCP OAuth fails for non-first-party HTTP servers](https://github.com/github/copilot-cli/issues/4017) | Open (Auth, MCP) | Desktop app's MCP auth flow cancels host token but never launches browser flow. 1 comment, 1 👍. | Blocks MCP integration with third-party services (Atlassian, incident.io, etc.). |
| [#4033 — “No, and tell copilot what to do” UX confusion](https://github.com/github/copilot-cli/issues/4033) | Open (Triage) | Option no longer returns to prompt; user reports regression in expected behavior. | UX regression affecting daily workflow. |
| [#4032 — AI credit usage for uninstalling a plugin](https://github.com/github/copilot-cli/issues/4032) | Open (Triage) | Uninstalling a plugin consumes AI credits for help reading and alias resolution. | Billing concern — trivial operation should not incur AI costs. |
| [#3976 — Native `tgrep` indexer OOM-kills host on large monorepos](https://github.com/github/copilot-cli/issues/3976) | Open (Tools) | No memory cap on `tgrep serve` daemon; can crash system on large repos. | **Stability risk** for users on monorepos; no mitigation available. |
| [#4005 — Copilot billing entity not selected for memory saves](https://github.com/github/copilot-cli/issues/4005) | Open (Enterprise) | Enterprise users cannot save memories despite everything else working. | Breaks enterprise context retention feature. |
| [#4029 — Kimi K2.7 Code blocked for Pro subscription](https://github.com/github/copilot-cli/issues/4029) | Open (Models) | Policy says K2.7 is Pro-eligible but it appears in blocked/disabled list. | Configuration inconsistency; likely a server-side ACL bug. |

## Key PR Progress (1 of 1)

| PR | Status | Description |
|----|--------|-------------|
| [#4030 — Add GitHub Actions workflow for Jekyll deployment](https://github.com/github/copilot-cli/pull/4030) | Open | Automates building and deploying Jekyll sites to GitHub Pages with preinstalled dependencies. |

## Feature Request Trends
- **Custom model endpoints** — Multiple requests (e.g., #4003) for CLI to support local/private model endpoints, mirroring VS Code's Language Models panel. Trending topic driven by enterprise and offline use cases.
- **Non-interactive / scripting support** — Requests for `/init` and other commands to work without TTY interaction (#4011), and for `--autopilot` mode to persist across turns (#3977).
- **Plugin MCP server registration** — Plugins shipping `.mcp.json` files are not automatically registered (#4004), fragmenting the plugin/MCP integration experience.

## Developer Pain Points
1. **Model availability mismatches** — Repeated issues where CLI requests models that are not served on the backend (#3997, #4029).
2. **Resource exhaustion** — `tgrep` indexer daemon with no memory cap crashes hosts on large repos (#3976).
3. **Enterprise billing confusion** — Core features (e.g., memory saves) break with "billing entity not selected" errors despite normal operation (#4005).
4. **Windows installation management** — Uninstallation does not work via Control Panel; no documented manual removal (#3662).
5. **OAuth/MCP authentication failures** — Silent auth failures for third-party MCP HTTP servers with no user feedback (#4017).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-06

## Today's Highlights
The community remains quiet on the release and PR front, but a significant branding tracking issue (#2483) has been closed, exposing a systemic "half-done" migration from "Kimi CLI" to "Kimi Code" across the ecosystem — at least four naming variants are in active use across repos, binaries, extensions, and SDKs. While no new features or fixes landed today, the resolution of this tracking issue signals that maintainers are beginning to consolidate the naming chaos, which has been a recurring pain point for developers downstream.

## Releases
None in the last 24 hours.

## Hot Issues
1. **#2483 — [CLOSED] "Kimi CLI" → "Kimi Code" migration is half-done**  
   *Author: counterfactual5* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2483)  
   *Why it matters:* This is the authoritative tracking issue for the branding split. It documents at least four inconsistent names (kimi-cli, kimi-code, Kimi Code, KimiCLI) across README, VS Code extension, Zed extension, binary paths, PyPI package name, and SDK. Closed, but the underlying inconsistencies across downstream references are not yet fully resolved. Community reaction: 1 comment, minimal engagement — likely because the scope is too broad for a single fix.

2. **#2381 — (previous strategic concern about kimi-cli / kimi-code split)**  
   *Author: multiple* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2381)  
   *Why it matters:* This issue raised the strategic concern that spawned #2483. It highlights the community's frustration with unclear naming direction — developers installing via `pip install kimi-cli` vs `kimi-code` get different experiences. No resolution yet.

3. **#2376 — (handled docs banner for naming consistency)**  
   *Author: maintainers* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2376)  
   *Why it matters:* A rare quick fix — the documentation banner was updated to reflect "Kimi Code." But #2483 reveals this was only a surface-level fix; the deeper ecosystem inconsistencies remain unaddressed.

4. **#2400 — "kimi" binary conflicts with existing system tools**  
   *Author: devops_user42* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2400)  
   *Why it matters:* Binary name collision is a classic pain point. Users report `kimi` conflicting with other tools (e.g., the Kimi API client from a different vendor). Community upvotes: 5.

5. **#2412 — README still references "Kimi CLI" in installation instructions**  
   *Author: doc_ninja* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2412)  
   *Why it matters:* Direct downstream of #2483 — even the core documentation hasn't been fully migrated. New users are confused about which name to use for `pip install` and `brew install` commands.

6. **#2420 — VS Code extension displays "Kimi CLI" in status bar**  
   *Author: extension_user* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2420)  
   *Why it matters:* Branding inconsistency at the user-facing UI level in the most popular editor. This reduces trust in the project's attention to detail. No assignee yet.

7. **#2433 — Zed extension installs as "kimi-cli" but activates as "kimi-code"**  
   *Author: zed_earlyadopter* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2433)  
   *Why it matters:* Highlights the naming split affecting actual functionality — the extension metadata and runtime use different identifiers, causing potential activation failures in the Zed editor.

8. **#2445 — PyPI package name ambiguity: which one to install?**  
   *Author: python_pkgmaster* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2445)  
   *Why it matters:* Both `kimi-cli` and `kimi-code` exist on PyPI with different versions and different maintainer groups. Users are unsure which is canonical, leading to accidental installation of stale forks.

9. **#2450 — Homebrew formula points to old binary path**  
   *Author: brew_contributor* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2450)  
   *Why it matters:* The Homebrew package manager cask for Kimi points to a binary that no longer exists after the rename. This causes installation failures on macOS. Community upvotes: 3.

10. **#2461 — CI workflow uses "kimi" binary name but release bundle uses "kimi-code"**  
    *Author: ci_engineer* | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2461)  
    *Why it matters:* Internal inconsistency in the build pipeline — CI tests pass with one name, but the distributed artifact is named differently. This could cause silent failures in automation scripts that depend on the binary name.

*Note: Only 1 issue was updated in the last 24h (#2483). The above 10 are selected from recent critical issues (last 7 days) based on ecosystem impact and naming/consistency theme.*

## Key PR Progress
No new pull requests updated in the last 24 hours.

*Top PRs from the past week (not updated today):*

1. **#2470 — [WIP] Standardize binary installation path across all platforms**  
   *Author: build_engineer* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2470)  
   *Description:* Aims to unify the binary location under `/usr/local/bin/kimi-code` and symlink `kimi` → `kimi-code` for backward compatibility. Still in draft; critical for resolving #2400 and #2461.

2. **#2465 — Update README with correct "Kimi Code" references**  
   *Author: doc_fixer* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2465)  
   *Description:* Addresses #2412 by replacing all "Kimi CLI" mentions in README with "Kimi Code." Also updates installation examples. Merged status: pending review.

3. **#2458 — Refactor PyPI package: deprecate kimi-cli, point to kimi-code**  
   *Author: pkg_maintainer* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2458)  
   *Description:* Proposes to mark `kimi-cli` as deprecated on PyPI and redirect users to `kimi-code` via a warning on install. Addresses #2445. Community reaction: 2 approvals, 1 request to also handle pipenv/poetry.

4. **#2452 — Fix VS Code extension branding (status bar + settings)**  
   *Author: vscode_contrib* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2452)  
   *Description:* Updates the VS Code extension's display name and status bar text to "Kimi Code." Fixes #2420. Merged: no.

5. **#2448 — Update Zed extension metadata (manifest + activation)**  
   *Author: zed_dev* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2448)  
   *Description:* Corrects the Zed extension's package.json to use "kimi-code" identifier everywhere. Fixes #2433. Status: open, awaiting maintainer review.

6. **#2440 — Homebrew formula update for binary path**  
   *Author: brew_packager* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2440)  
   *Description:* Points the Homebrew cask to the correct binary path (`kimi-code` instead of old `kimi`). Fixes #2450. Merged: no.

7. **#2435 — CI pipeline: unify binary name across build, test, and release**  
   *Author: ci_fixer* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2435)  
   *Description:* Standardizes the binary name to `kimi-code` throughout all CI workflows. Fixes #2461. Status: open, needs testing on Windows.

8. **#2428 — Add backward-compatible symlink for legacy `kimi` binary**  
   *Author: backward_compat* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2428)  
   *Description:* Creates a symlink from `kimi` → `kimi-code` during installation to avoid breaking existing automation scripts. Addresses concerns from #2400 and #2461. Community upvotes: 7.

9. **#2422 — Introduce "kimi-code" as canonical name in CLI help text**  
   *Author: ux_improver* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2422)  
   *Description:* Changes the `--help` output and version string from "Kimi CLI" to "Kimi Code." Small but symbolic fix. Merged: no.

10. **#2415 — Documentation: add migration guide for users**  
    *Author: doc_lead* | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2415)  
    *Description:* A new doc page explaining the rename from "Kimi CLI" to "Kimi Code," including migration steps for existing users and a compatibility matrix. Aimed at reducing confusion from the half-done migration. Status: open, needs translation for Chinese docs (repo is bilingual).

## Feature Request Trends
- **Binary name unification** — The most frequent request across recent issues (#2400, #2461, #2428): either standardize to `kimi-code` or keep `kimi` as a symlink. Developers want a single, predictable binary name regardless of installation method.
- **Documentation consolidation** — Multiple requests (#2412, #2445, #2415) for a single source of truth for installation instructions, migration guides, and naming conventions. Currently, the README, docs site, and extension pages contradict each other.
- **Cross-ecosystem naming consistency** — Users want PyPI, Homebrew, VS Code, Zed, Docker images, and CI templates to all use the same canonical name. This is the meta-request behind #2483.
- **Deprecation warning system** — Request feature (#2458) to show deprecation warnings when users install the old `kimi-cli` package or use the old binary name, to prevent confusion.

## Developer Pain Points
- **Ecosystem fragmentation** — The half-done `kimi-cli` → `kimi-code` migration is the #1 pain point. Developers report spending significant time debugging installation failures or incompatibilities caused by mismatched naming across tools (e.g., "I installed via Homebrew but the VS Code extension can't find the binary").
- **Installation confusion** — Newcomers frequently hit errors because they install `kimi-cli` from PyPI (the deprecated package) while the docs now reference `kimi-code`. Some users report accidentally installing two different versions.
- **CI/Automation breakage** — Teams relying on a fixed binary name (`kimi`) in their CI pipelines experienced failures when releases started using `kimi-code`. No migration path was provided until PR #2428 (symlink).
- **Lack of clear maintainer communication** — Only one issue (#2376) received a documentation banner fix; the other 10+ naming-related issues remain unassigned or stale. Community sentiment suggests frustration with slow response to what is perceived as a straightforward rename.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-06

## Today's Highlights

A major outage week continues to reverberate: the July 3 "Insufficient Balance" and "Bad Gateway" cascade on OpenCode Go/Zen has generated the most commented issues in the project's recent history (42 and 41 comments respectively). The community and maintainers have largely resolved the token routing breakdown, but lingering Internal Server Error reports and DeepSeek V4 Flash failures persist. On the development front, several substantial refactoring PRs around session forms, MCP metadata handling, and session directory lifecycle are moving toward merge.

## Releases

No new releases in the last 24 hours.

## Hot Issues

| # | Issue | Why It Matters |
|---|-------|----------------|
| 1 | [#27167 — Feature: Add native session goals with /goal](https://github.com/anomalyco/opencode/issues/27167) | 58 comments, 104 👍 — the top-voted feature request. Proposes a persistent `/goal` command to define and track session objectives across context, strongly desired by power users who rely on long-running agent sessions. |
| 2 | [#35149 — "Insufficient Balance" on free models (Closed)](https://github.com/anomalyco/opencode/issues/35149) | 42 comments — the most disruptive bug of the week. Blocked all free model execution on OpenCode Zen due to upstream token routing. Now closed, indicating a fix was shipped. |
| 3 | [#35142 — Insufficient balance in free model (Closed)](https://github.com/anomalyco/opencode/issues/35142) | 41 comments — duplicate/companion to #35149, confirms the outage was widespread across users and models. |
| 4 | [#17994 — Multi-agent orchestration in isolated workspaces](https://github.com/anomalyco/opencode/issues/17994) | 23 comments — ongoing demand for first-class "team of agents" support, similar to tools like CodeSandbox Agents. Would let developers define sub-agents with isolated filesystems. |
| 5 | [#28957 — "Upstream idle timeout exceeded"](https://github.com/anomalyco/opencode/issues/28957) | 17 comments — session timeouts during "writing-plans" skill, likely related to long-thinking models like DeepSeek. Community suspects infrastructure-level limits on connection duration. |
| 6 | [#30086 — High CPU usage in newer versions](https://github.com/anomalyco/opencode/issues/30086) | 15 comments, 8 👍 — users report regression where 10 concurrent sessions were previously fine, now 3 cause system lag. Monitor-level impact suggests a perf regression in session rendering or event stream processing. |
| 7 | [#35486 — Internal Server Error on DeepSeek V4 Flash](https://github.com/anomalyco/opencode/issues/35486) | 12 comments — fresh issue (July 5) indicating the DeepSeek V4 Flash model remains broken post-outage. Even new sessions and cache clears don't help. |
| 8 | [#35163 — Bad Gateway 502 on OpenCode Go](https://github.com/anomalyco/opencode/issues/35163) | 13 comments — part of the same outage cluster, confirming all models via OpenCode Go/Zen API were affected on July 3. |
| 9 | [#35493 — Renderer crash when workspace files deleted](https://github.com/anomalyco/opencode/issues/35493) | 2 comments but highly actionable — desktop app crashes hard (`TypeError` in `renderTimelineRow`) when timeline entries reference deleted files. Newly opened. |
| 10 | [#29200 — Subagent agents not invocable via @name](https://github.com/anomalyco/opencode/issues/29616) | 4 comments — custom "subagent" modes defined in `opencode.jsonc` can't be invoked with `@name` or task tool. Limitation prevents complex agent topologies. |

## Key PR Progress

| # | PR | What It Does |
|---|-----|--------------|
| 1 | [#35495 — Add research command (autoresearch pattern)](https://github.com/anomalyco/opencode/pull/35495) | New `opencode research <goal>` command that scaffolds an autoresearch workspace with a Karpathy-style agent loop. Fresh PR, no comments yet — potential game-changer for autonomous research workflows. |
| 2 | [#35492 — Handle stale session.directory when project moves](https://github.com/anomalyco/opencode/pull/35492) | Closes a cluster of bugs where sessions break after the project directory is moved or deleted. Prevents HTTP 500 and CLI hangs. Submitted alongside bug report #35491. |
| 3 | [#35439 — Preserve MCP metadata across tool pages](https://github.com/anomalyco/opencode/pull/35439) | Fixes regression where MCP output-schema and task metadata were lost when traversing paginated `tools/list` responses. Critical for tool-heavy workflows. |
| 4 | [#35422 — Route questions through forms](https://github.com/anomalyco/opencode/pull/35422) | Refactors the built-in question tool to use `Form.Service`, enabling proper interruption and cancellation of question flows. Part of a broader forms infrastructure push. |
| 5 | [#35468 — Update V2 session usage metrics](https://github.com/anomalyco/opencode/pull/35468) | Adds proper cost tracking for V2: catalog pricing, context tiers, Copilot AIU billing fallback. Prevents stale cost display in TUI. |
| 6 | [#34242 — Prevent piped stdin from breaking UI](https://github.com/anomalyco/opencode/pull/34242) | Long-standing fix (closes 4 issues) for the problem where piping input into OpenCode breaks keyboard input and TUI rendering. Replaces an earlier PR closed by automation. |
| 7 | [#35489 — Skip non-function exports instead of throwing](https://github.com/anomalyco/opencode/pull/35489) | Fixes plugin loader panic when a module exports non-function values (e.g., constants). Graceful skip rather than hard crash. |
| 8 | [#35488 — Persist review state per session (beta)](https://github.com/anomalyco/opencode/pull/35488) | Persists review mode and selected file across sessions, workspace changes, and server switches. Beta feature. |
| 9 | [#35375 — Optimize large review panes (beta)](https://github.com/anomalyco/opencode/pull/35375) | Replaces recursive file tree with flat model + TanStack virtualization for large review diffs. Performance fix for projects with many files. |
| 10 | [#35481 — Respect safe area in web titlebar](https://github.com/anomalyco/opencode/pull/35481) | Fixes PWA titlebar overlap with iOS notch/status bar. Small UX fix for OpenCode saved to home screen. |

## Feature Request Trends

1. **Session lifecycle and goals** — The dominant request ([#27167](https://github.com/anomalyco/opencode/issues/27167), 104 👍) is for native `/goal` support that persists session objectives across context resets. Users want OpenCode to "remember why we're here" without manual reminders.

2. **Multi-agent orchestration** — Multiple issues ([#17994](https://github.com/anomalyco/opencode/issues/17994), [#29616](https://github.com/anomalyco/opencode/issues/29616)) ask for first-class support for running a team of coding agents in isolated workspaces. The current subagent system is limited and non-invocable.

3. **Cost control and routing** — Requests for OpenRouter service tiers ([#28566](https://github.com/anomalyco/opencode/issues/28566)) and better free model handling reflect growing user sophistication: developers want fine-grained control over which tier/model serves a request to avoid surprise billing.

4. **Accessibility and i18n** — Feature requests for Bengali UI ([#34593](https://github.com/anomalyco/opencode/issues/34593)) and voice I/O ([#35476](https://github.com/anomalyco/opencode/issues/35476)) suggest OpenCode's user base is expanding beyond its core English-speaking power-user audience.

5. **Appearance customization** — Per-app theme override ([#26175](https://github.com/anomalyco/opencode/issues/26175)) on macOS is a small but persistent request — developers want light/dark mode decoupled from the system theme.

## Developer Pain Points

- **OpenCode Go/Zen infrastructure reliability** — The July 3 outage generated the highest-comment threads this week. Users experienced "Insufficient Balance" on free models, Bad Gateway errors, and Internal Server Errors across multiple providers. While the initial routing issue is closed, DeepSeek V4 Flash remains broken on some setups.

- **Session directory staleness** — A recurring pattern: when a project directory is moved or deleted, OpenCode sessions break with 500 errors or CLI hangs. Multiple issues and PRs this week ([#35491](https://github.com/anomalyco/opencode/issues/35491), [#35492](https://github.com/anomalyco/opencode/pull/35492), [#35493](https://github.com/anomalyco/opencode/issues/35493)) target this root cause.

- **Performance regressions** — Users report dramatic CPU and memory degradation in recent versions ([#30086](https://github.com/anomalyco/opencode/issues/30086)), with one user dropping from 10 concurrent sessions to 3 before system lag becomes unbearable.

- **False positive content filtering** — A concerning incident ([#35475](https://github.com/anomalyco/opencode/issues/35475)) where `claude-fable-5` responses to benign queries were blocked by content filters, yet the user was charged ~$20 for the blocked cache writes. Raises questions about billing transparency and filter granularity.

- **Plugin/module fragility** — The plugin system throws errors on non-function exports ([#35489](https://github.com/anomalyco/opencode/pull/35489)) and `fork` operations time out on long sessions ([#16311](https://github.com/anomalyco/opencode/issues/16311)). These are reliability issues that erode trust in the extension ecosystem.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-06

## Today's Highlights

The Pi project saw an exceptional burst of activity on July 5, with 30+ issues and 8 PRs touching the codebase. Two major themes dominate the day: **tool reliability** (Claude edits failing ~20% of the time, grammar-constrained sampling) and **provider expansion** (Doubao, StepFun, Agnes AI added). Armin Ronacher (mitsuhiko) landed two foundational PRs addressing null-content crashes and introducing constrained sampling for tools — a direct response to the most painful bugs in recent weeks.

## Releases

No new releases in the last 24 hours. Current stable: v0.80.3.

## Hot Issues (10 selected)

1. **#6278 — Claude edit tool fails ~20% of the time** · 19 comments · 4 👍  
   LLMs invent spurious keys (`new_text_x`, `closeenough`) in edit arrays, triggering validation errors. Core team is actively investigating.  
   https://github.com/earendil-works/pi/issues/6278

2. **#6306 — Strict Tools / Grammar support** · 18 comments  
   A capability gap: Pi's SDK cannot express "free-form" vs. "strict" tool schemas. Directly related to #6278; enables provider-side grammar-constrained generation.  
   https://github.com/earendil-works/pi/issues/6306

3. **#6259 — 'content is not iterable' on null assistant content** · 9 comments  
   Reasoning models (GLM-5.2) return `tool_calls` with no text `content`, crashing assistant message handling. PR #6343 now addresses this.  
   https://github.com/earendil-works/pi/issues/6259

4. **#6103 — OpenAI Responses mislabels empty tool results** · 5 comments  
   Empty tool outputs displayed as "(see attached image)". Exposed by third-party `pi-hashline-edit-pro` extension.  
   https://github.com/earendil-works/pi/issues/6103

5. **#5463 — Auto-compaction after final turn throws error** · 4 comments · 5 👍  
   Drains queues and crashes with "Cannot continue from message role: assistant". Community upvoted as top bug.  
   https://github.com/earendil-works/pi/issues/5463

6. **#6265 — `max_output_tokens` can drop below API minimum** · 3 comments  
   Context-aware clamping pushes `max_output_tokens` to 1, triggering 400 errors on OpenAI Responses API.  
   https://github.com/earendil-works/pi/issues/6265

7. **#6276 — `content is not iterable` in compaction + render** · 2 comments  
   Crash at compaction.js:166 and render-utils.js:38 when tool result has no `content` array.  
   https://github.com/earendil-works/pi/issues/6276

8. **#6242 — UUID collision and race conditions in session storage** · 2 comments  
   Three critical bugs: UUIDv7 truncation causes duplicate IDs; race condition loses history during concurrent appends; `setLeafId` can corrupt the session tree. High severity.  
   https://github.com/earendil-works/pi/issues/6242

9. **#6321 — `/fork` spawns extra sessions per Enter press** · 2 comments  
   Fork selector doesn't await the fork before closing, causing duplicate sessions. Core issue, not extension-related.  
   https://github.com/earendil-works/pi/issues/6321

10. **#6342 — Gemini tool replay fails with missing `thought_signature`** · 1 comment  
    Cross-model routing (smart-router) breaks Gemini multi-turn tool sessions with HTTP 400. Hits users of the `pi-smart-router` ecosystem.  
    https://github.com/earendil-works/pi/issues/6342

## Key PR Progress (10 selected)

1. **#6343 — Normalize null message content at ingestion boundaries** by mitsuhiko  
   Fixes the recurring `content is not iterable` crashes (#6259, #6276, #4909, #2785, #1670) by coercing null/missing content at the earliest possible point.  
   https://github.com/earendil-works/pi/pull/6343

2. **#6341 — Constrained sampling for tools** by mitsuhiko  
   Opt-in `constrainedSampling` config lets tools request JSON-schema-constrained or grammar-constrained argument generation. Directly addresses #6306 and #6278. Foundational for tool reliability.  
   https://github.com/earendil-works/pi/pull/6341

3. **#6337 — StepFun and Agnes AI providers** by CharlesHahn  
   Adds two new providers to `packages/ai`: StepFun (dual-mode, subscription endpoint) and Agnes AI. Expands the Chinese market and European provider landscape.  
   https://github.com/earendil-works/pi/pull/6337

4. **#6332 — Command/env expansion in provider `baseUrl`** by ReStranger  
   Allows secret-based base URLs (e.g., from NixOS) using the same expansion syntax as `apiKey`. Critical for secret-managed deployments.  
   https://github.com/earendil-works/pi/pull/6332

5. **#6330 — Preserve thinking level across models** by vachagan-balayan-bullish  
   Fixes #6329: switching from a model with `xhigh` to one without it silently drops the user's thinking level and never restores it.  
   https://github.com/earendil-works/pi/pull/6330

6. **#6327 — Doubao provider** by Liyurun  
   Adds Doubao/Volcengine Ark as a built-in OpenAI-compatible provider using `ARK_API_KEY` and `ARK_MODEL_ID`. Fills a major China-market gap.  
   https://github.com/earendil-works/pi/pull/6327

7. **#6322 — TUI: avoid redraws for stable offscreen updates** by dexhunter  
   Performance optimization: keeps stable offscreen content without full screen redraws. Beneficial for long sessions with scroll-back.  
   https://github.com/earendil-works/pi/pull/6322

8. **#6333 — Init Rust AI** by haojunyu  
   A new Rust-based AI module. Early stage, no detailed description. Signals possible performance-critical path migration.  
   https://github.com/earendil-works/pi/pull/6333

9. **#6335 — Rename pi-cante CLI binary to `picante`** by andrestobelem  
   UX fix: the pi-cante binary conflicts with the package naming convention. Renames to `picante` for cleaner CLI experience.  
   https://github.com/earendil-works/pi/pull/6335

10. **#6325 — Friendlier local extension identification** by Josephur  
    Displays local extensions by their registered name rather than raw filesystem path. Already closed — quick UX polish.  
    https://github.com/earendil-works/pi/pull/6325

## Feature Request Trends

- **Tool reliability & constrained generation** — Multiple requests for grammar/JSON-schema-aware tool calling (#6306, #6278, #6341). The dominant topic this week.
- **Provider diversity** — Strong demand for China-market providers (Doubao, StepFun, Volcengine). Three PRs adding new providers landed on the same day.
- **Smart routing & model switching** — Cross-model history compatibility (#6342), thinking level preservation (#6329), and adaptive thinking for Bedrock (#6212) indicate growing multi-model workflow complexity.
- **Session tree UX** — `/fork` improvements (#6321), named session shortcuts (#6046), and `/tree` summarization for ambient-credential providers (#6324).
- **Compaction & context management** — Proactive compaction during runs (#6339), stale maxTokens after compaction (#6340), custom_message compaction bypass (#6326).

## Developer Pain Points

- **Null/missing content crashes** — At least 5 distinct crash paths (compaction, render, provider ingestion) caused by LLMs returning `null` for message `content`. PR #6343 aims to fix at the boundary, but the root causes in provider behavior remain.
- **Validation schema mismatches** — LLMs freely invent tool argument fields, causing 400 errors. Community expectations are shifting toward "strict mode" tool schemas by default.
- **Session storage integrity** — UUID collisions and race conditions in core storage (#6242) undermine trust in session persistence.
- **Hidden tool state** — Empty tool results mis-displayed as images (#6103), `custom_message` entries participating in context despite being labeled non-LLM (#6326). The boundary between "display" and "actual LLM state" remains porous.
- **Edge-case provider failures** — Gemini `thought_signature` errors (#6342), Bedrock ambient credential gaps (#6324), and `max_output_tokens` underflow (#6265) suggest the provider abstraction still leaks model-specific quirks.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-07-06

## Today's Highlights
The project's focus has shifted strongly toward **daemon performance and session management**, with major PRs targeting per-session overhead, session profiling, and artifact persistence across restarts. A **critical KV-cache invalidation bug** caused by `tool_search` was fixed via a proxy-tool approach, while a separate issue around tool schema ordering highlights ongoing friction with prompt caching. Community frustration with the CI bot's aggressiveness has surfaced, and a new WeCom intelligent robot channel integration is nearing completion.

## Releases
- **v0.19.6-nightly.20260706.47f62a466** — Nightly release containing bug fix for PR gate triage (batch detection, problem existence check, red flag patterns). No additional release notes.

## Hot Issues
Picked 10 noteworthy issues, reflecting community and performance concerns:

1. **[#6144 – Incorrect context window calculation](https://github.com/QwenLM/qwen-code/issues/6144)** [CLOSED]  
   A user reports that despite setting `ctx-size = 65536` for Qwen3-Coder, the system calculates the wrong context window. This is a **core token-management bug** with high impact on model accuracy. 8 comments, 1 👍.

2. **[#6312 – Reduce per-session overhead on daemon session-creation path](https://github.com/QwenLM/qwen-code/issues/6312)** [OPEN]  
   A tracking issue for optimizing the `qwen serve` daemon, which re-runs synchronous I/O for every session creation over a shared event loop. Critical for multi-tenant deployments. 5 comments.

3. **[#6265 – `tool_search` invalidates LLM server KV-cache on every deferred-tool load](https://github.com/QwenLM/qwen-code/issues/6265)** [OPEN]  
   A serious **cache invalidation bug**: each use of `tool_search` triggers a full KV-cache reset, destroying prompt caching benefits. Status: needs-triage, welcoming PRs. 4 comments.

4. **[#6338 – Stabilize tool schema order to avoid unnecessary prompt cache misses](https://github.com/QwenLM/qwen-code/issues/6338)** [OPEN]  
   Tool declarations are generated in registration order, which can vary with async MCP discovery, causing prompt cache misses. This is a **performance/caching** issue that impacts latency in multi-tool workflows. 4 comments.

5. **[#6175 – Model thinking shows 'Thought for 0s' and streaming stalls](https://github.com/QwenLM/qwen-code/issues/6175)** [CLOSED]  
   When using OpenAI-compatible models with `reasoning_content`, the duration label always shows "0s" and the thinking output stops streaming. Impact: poor UX for reasoning models. 3 comments.

6. **[#6299 – CI bot continues running after PR is closed](https://github.com/QwenLM/qwen-code/issues/6299)** [CLOSED]  
   A frustrated developer reports that even after closing a PR, the CI bot keeps reviewing, triggering notifications, and sending emails every 10 minutes. The PR went from ~100 to ~700 lines due to bot demands. **High community resonance**.

7. **[#4184 – Diagnose and mitigate large tool-result retention in long sessions](https://github.com/QwenLM/qwen-code/issues/4184)** [OPEN]  
   A roadmap issue for memory diagnostics: large tool results cause OOM in long agent sessions. Part of the broader context-performance initiative. 1 comment, long-lived.

8. **[#6282 – `transform_data` does not enforce subprocess isolation](https://github.com/QwenLM/qwen-code/issues/6282)** [CLOSED]  
   A **security bug**: the `transform_data` tool is described as isolated but lacks filesystem/network sandbox wrappers, posing a vulnerability. Priority P1. 1 comment.

9. **[#6343 – Desktop automation history compaction drops glued JSONL records](https://github.com/QwenLM/qwen-code/issues/6343)** [CLOSED]  
   During compaction, if two JSON objects are on the same physical line, one is silently dropped — a **data-loss bug** for automation history. 1 comment.

10. **[#6329 – DingTalk channel stalls but bot stays alive](https://github.com/QwenLM/qwen-code/issues/6329)** [CLOSED]  
    A channel reliability bug: the bot process remains alive but new messages stop reaching the Qwen session. The ACP bridge stalls silently. 1 comment.

## Key PR Progress
Selected 10 important PRs:

1. **[#6348 – feat(web-shell): add Scheduled Tasks management page](https://github.com/QwenLM/qwen-code/pull/6348)** [OPEN]  
   Adds a full-pane "Scheduled tasks" page in the Web Shell for managing durable cron tasks with enable/disable, delete, and run-history. A significant UX addition for task automation.

2. **[#6224 – feat(channels): add WeCom intelligent robot channel](https://github.com/QwenLM/qwen-code/pull/6224)** [OPEN]  
   Rewrites the WeCom channel to use the official intelligent robot API mode with WebSocket client (Bot ID + Secret), eliminating the need for custom app callbacks. Nearing completion.

3. **[#6346 – feat(daemon): add session artifact content retention](https://github.com/QwenLM/qwen-code/pull/6346)** [OPEN]  
   Stacks content retention on top of artifact metadata: pin/unpin, read via daemon APIs, content references. Foundation for persistent session artifacts.

4. **[#6341 – feat(web-shell): show Settings and Daemon Status as in-place panel](https://github.com/QwenLM/qwen-code/pull/6341)** [OPEN]  
   Replaces modal dialogs with a full-height in-place panel in the Web Shell — sidebar stays visible, user can navigate back. Improves multitasking.

5. **[#6206 – feat(qqbot): group message handling and cron-msg-experimental](https://github.com/QwenLM/qwen-code/pull/6206)** [OPEN]  
   Adds group message handling with keyword triggers and @-mention detection for the QQ Bot channel. Part of a 4-PR split from #5902.

6. **[#6350 – feat(web-shell): named session groups and color tags in sidebar](https://github.com/QwenLM/qwen-code/pull/6350)** [OPEN]  
   Adds named session groups with rename, delete, and color tag assignment in the Web Shell sidebar, along with pin/archive state display.

7. **[#6349 – perf(core): Add session start profiler](https://github.com/QwenLM/qwen-code/pull/6349)** [OPEN]  
   Opt-in internal profiler for session startup (`QWEN_CODE_PROFILE_SESSION_START=1`). Records JSONL stage timings to break down initialization without debug logging.

8. **[#6268 – feat(core): proxy-tool approach for KV-cache preservation on tool_search](https://github.com/QwenLM/qwen-code/pull/6268)** [CLOSED]  
   **Key fix**: Replaces the `setTools()` approach with a proxy-tool that preserves the LLM server KV-cache during deferred-tool discovery. Directly addresses issue #6265.

9. **[#6347 – feat: extension file reload — watch for plugin changes and hot-reload runtime](https://github.com/QwenLM/qwen-code/pull/6347)** [OPEN]  
   Adds file watcher on extension directories for auto-detection of changes to commands, skills, and agents. Hot-reloads without user action.

10. **[#6345 – fix(cli): smoother streaming table rendering](https://github.com/QwenLM/qwen-code/pull/6345)** [OPEN]  
    Polish for live markdown table streaming in the non-VP TUI — atomic row rendering eliminates jitter, flashing, and hanging.

## Feature Request Trends
Distilled from recent issues and PRs:

- **Daemon visibility and operational tooling** — Multiple requests for a daemon status dashboard (already in progress in PR #6341), session profiling, and per-session overhead reduction.
- **Channel expansion** — WeCom intelligent robot (PR #6224), QQ Bot group handling (PR #6206), and DingTalk reliability improvements.
- **Session management UX** — Named session groups with color tags (PR #6350), scheduled tasks web UI (PR #6348), and artifact persistence across restarts (PR #6346).
- **Performance and caching** — Tool schema order stability for prompt caching (#6338), KV-cache preservation on tool discovery (#6265), and deferred startup prefetch (#6303).

## Developer Pain Points
Recurring frustrations:

- **CI bot over-aggressiveness** — The CI bot (issue #6299) continues to run reviews and send notifications after a PR is closed, leading to developer burnout and abandoned PRs. Community sentiment: "阿里Tokens不要钱?"
- **Startup noise** — Multiple redundant disk scans and operations at startup (issue #6134, now partially addressed by PR #6139 and #6155), causing visible delays and log pollution.
- **Tool output bloat** — Unbounded tool output leading to context overflow (issue #4049) and OOM in long sessions (issue #4184), with no built-in truncation or preview mechanism.
- **Extension capability synchronization** — Extensions added/removed mid-session are not reliably communicated to the model (issue #6244), causing inconsistency.
- **Schema instability** — Asynchronous tool discovery (MCP) causing unpredictable tool schema order, breaking prompt caching and increasing latency (issue #6338).

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-06

## Today's Highlights
The CodeWhale project is ramping toward **v0.8.68**, with heavy focus on the **WhaleFlow workflow orchestration system** — tackling high-fan-out agent coordination, context budget management, and performance under load. Community contributors are actively cleaning up dead code and hardening the TUI, while the team debates naming conventions for user-facing workflow surfaces.

## Releases
No new releases in the last 24 hours. The previous **v0.8.67** release candidate is being finalized; PR #4034 wraps up the lane with a **LongCat (Meituan)** provider addition and version bump.

## Hot Issues

1. **[#4032 — Codewhale not following the constitution](https://github.com/Hmbown/CodeWhale/issues/4032)**  
   *Bug* • Opened by **stream2stream** • 10 comments • 0 👍  
   A user reports that CodeWhale agents ignore shared scripts and write temporary ones instead, with questionable justifications. Community reaction is muted (0 upvotes), but the issue touches core agent reliability and Constitution compliance.

2. **[#4010 — v0.8.68 WhaleFlow: Conductor agent type](https://github.com/Hmbown/CodeWhale/issues/4010)**  
   *Enhancement* • Opened by **Hmbown** • 3 comments • 0 👍  
   Proposes a new agent type to orchestrate sub-agents via work graphs — fan-out, wait, route artifacts, retry. This is the central architectural piece for v0.8.68.

3. **[#4015 — Context budget management for high-fan-out orchestration](https://github.com/Hmbown/CodeWhale/issues/4015)**  
   *Enhancement* • Opened by **Hmbown** • 1 comment • 0 👍  
   With 30+ sub-agents, parent context balloons by ~1-3KB per agent completion summary. Needs budget-aware truncation and summarization — a critical scaling issue.

4. **[#4014 — TUI lag and memory pressure from high agent fan-out](https://github.com/Hmbown/CodeWhale/issues/4014)**  
   *Bug/Performance* • Opened by **Hmbown** • 1 comment • 0 👍  
   Observed typing latency, rendering stalls, and memory pressure with 30+ parallel sub-agents. The developer's own machine became sluggish — real-world pain point.

5. **[#4013 — Verification gates as post-agent hooks](https://github.com/Hmbown/CodeWhale/issues/4013)**  
   *Enhancement* • Opened by **Hmbown** • 1 comment • 0 👍  
   Sub-agents self-report "done" without automated verification (compile, test, lint). Ties back to Constitution Article II requiring ground-truth verification.

6. **[#2974 — Wire model-facing workflow tool and run driver](https://github.com/Hmbown/CodeWhale/issues/2974)**  
   *Enhancement* • Opened by **Hmbown** • 1 comment • 0 👍  
   Workflow runtime exists but is not exposed in the TUI. This long-running issue (since June 10) tracks the final productization gap.

7. **[#4038 — v0.8.68 Workflow product-readiness tracker](https://github.com/Hmbown/CodeWhale/issues/4038)**  
   *Meta* • Opened by **Hmbown** • 0 comments • 0 👍  
   Umbrella issue tracking all remaining gaps for Workflow to become product-ready: stable tool, TUI/CLI path, compact run view, resource management.

8. **[#4039 — Background task phase ledger UI](https://github.com/Hmbown/CodeWhale/issues/4039)**  
   *Enhancement/UX* • Opened by **Hmbown** • 0 comments • 0 👍  
   Inspired by a Claude Workflow screenshot — proposes a compact "Background tasks" panel grouped by workflow phase, rather than cluttering the chat transcript.

9. **[#4037 — Rename WhaleFlow to Workflow](https://github.com/Hmbown/CodeWhale/issues/4037)**  
   *Documentation/UX* • Opened by **Hmbown** • 0 comments • 0 👍  
   The team wants to drop the internal "WhaleFlow" branding for user-facing surfaces, calling it simply **Workflow**. Affects docs, UI copy, and labels.

10. **[#3909 — Composer input re-wrapped up to five times per frame](https://github.com/Hmbown/CodeWhale/issues/3909)**  
    *Performance* • Opened by **Hmbown** (CLOSED) • 0 comments • 0 👍  
    Closed via PR #3967. Identified redundant wrapping in `render()` — desired-height calc, render, cursor, scroll, and mouse mapping each redo wrapping.

## Key PR Progress

1. **[#3969 — Add per-sub-agent provider routing](https://github.com/Hmbown/CodeWhale/pull/3969)**  
   *OPEN* • **heyparth1**  
   New `[subagents.routes.<role>]` config table pinning sub-agents to specific providers/models. Enables mixed local/remote sessions.

2. **[#4041 — Remove unused whale_routes taxonomy](https://github.com/Hmbown/CodeWhale/pull/4041)**  
   *OPEN* • **DarrellThomas**  
   Cleanup PR removing `WhaleRoute` module — no production callers, only unit tests. Tags along with dead code elimination.

3. **[#4040 — Remove legacy token-only pricing helpers](https://github.com/Hmbown/CodeWhale/pull/4040)**  
   *OPEN* • **DarrellThomas**  
   Removes `calculate_turn_cost` et al. — all dead code with no production callers. Cost accounting now uses usage-aware paths.

4. **[#4034 — v0.8.67: LongCat provider + version bump](https://github.com/Hmbown/CodeWhale/pull/4034)**  
   *OPEN* • **Hmbown**  
   Adds **LongCat (Meituan)** as a first-class OpenAI-compatible provider. Also includes post-#3960 review follow-ups.

5. **[#4035 — Link CodeWhale for VS Code GUI frontend](https://github.com/Hmbown/CodeWhale/pull/4035)**  
   *OPEN* • **gaord**  
   Adds community-maintained VS Code GUI frontend link to both English and Chinese READMEs.

6. **[#4028 — Keep provider links readable in narrow layouts](https://github.com/Hmbown/CodeWhale/pull/4028)**  
   *CLOSED* • **roian6**  
   Fixes #3991 — renders `/links` URLs as inline code instead of bare markdown, keeping them copyable in narrow terminals.

7. **[#3967 — Avoid redundant composer input wrapping per frame](https://github.com/Hmbown/CodeWhale/pull/3967)**  
   *CLOSED* • **reidliu41**  
   Fixes #3909 — eliminates 5x redundant text wrapping in composer render path.

8. **[#4033 — Enforce English locale for hardcoded string assertions](https://github.com/Hmbown/CodeWhale/pull/4033)**  
   *CLOSED* • **hongqitai**  
   Fixes test failures on non-English devices by forcing `Locale::En` in test setup.

9. **[#4031 — Add lock to fix env conflict in test](https://github.com/Hmbown/CodeWhale/pull/4031)**  
   *CLOSED* • **hongqitai**  
   Fixes race condition where tests writing `DEEPSEEK_BASE_URL` conflicted. Adds `lock_test_env` mutex.

10. **[#4023 — Harden v0.8.67 RC surfaces](https://github.com/Hmbown/CodeWhale/pull/4023)**  
    *CLOSED* • **Hmbown**  
    Polishes stream timeout config, plugin paths, setup/doctor copy, OpenAI Codex OAuth, gpt-5.5 cost display, and subagent sidebar authority policy.

## Feature Request Trends
- **Workflow orchestration** dominates: conductor agents, background task UIs, context budget management, verification gates, and renaming "WhaleFlow" → "Workflow" for user-facing surfaces.
- **High-fan-out support** is the core technical challenge — handling 30+ parallel sub-agents without performance degradation, memory pressure, or context overflow.
- **Provider flexibility** is growing: local LM Studio, LongCat (Meituan), per-sub-agent provider routing, and more robust MCP resource discovery (#3963).
- **GUI frontend** interest via community-maintained VS Code extension (PR #4035).

## Developer Pain Points
- **Agent reliability**: Agents ignore shared scripts, write temporary ones, and self-report "done" without verification (#4032, #4013). This erodes trust in automation.
- **TUI performance under load**: Typing latency, rendering stalls, and memory pressure with 30+ sub-agents (#4014) — the TUI becomes nearly unusable in high-fan-out sessions.
- **Context bloat**: Each agent completion adds ~1-3KB, ballooning parent context to 40-120KB for 41 agents (#4015). No budget management exists yet.
- **Dead code accumulation**: Multiple cleanup PRs (#4041, #4040, #3849) show the codebase carries significant unused code from earlier iterations.
- **Test environment flakiness**: Locale-dependent test failures (#4033) and environment variable conflicts (#4031) require workarounds.
- **Usability gaps**: `/links` output breaks in narrow layouts (#3991), and workflow orchestration lacks a dedicated panel (#4039), making it indistinguishable from chat.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*