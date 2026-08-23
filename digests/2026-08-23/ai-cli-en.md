# AI CLI Tools Community Digest 2026-08-23

> Generated: 2026-08-23 00:32 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Tool Comparison Report
**Date: 2026-08-23**

---

## 1. Ecosystem Overview

The AI CLI tools landscape is entering a stabilization phase punctuated by targeted hardening. Claude Code shipped a quiet maintenance release while its community converges on multi-account support as the dominant unmet need. OpenAI Codex is actively iterating on alpha releases with a focus on thread-source attribution and runtime safety. Gemini CLI shipped a critical macOS sandbox escape fix, signaling a maturing security posture, while smaller tools like Kimi Code and Pi show growing communities with distinct platform and UX pain points. Across all tools, agent reliability—particularly false success signals and silent failures—has emerged as the most consistent developer concern, outpacing feature requests in urgency.

---

## 2. Activity Comparison

| Tool | Hot Issues (Active) | PRs (24h) | Release Status |
|---|---|---|---|
| **Claude Code** | 10 tracked; 2 issues at 1,105 combined upvotes | 0 merged/updated | v2.1.240 (stable, maintenance) |
| **OpenAI Codex** | 10 tracked; top issue 394 👍 | 5 active PRs | 2 alpha releases (rust-v0.150.0-alpha.7, rust-v0.149.0-alpha.7.2) |
| **Gemini CLI** | 10 tracked; 4 P1 issues | 10 PRs (2 closed/merged) | v0.56.0-nightly (nightly) |
| **Copilot CLI** | 7 tracked + 3 new triage | 0 updated | No release |
| **Kimi Code** | 2 hot issues + 1 closed | 2 PRs (1 merged) | No release |
| **OpenCode** | 10 tracked; memory megathread 104 👍 | 10 PRs (5 merged) | No release; latest v1.18.21 |
| **Pi** | 10 tracked; auto-compaction bug 18 👍 | 10 PRs (6 closed/merged) | No release; v0.84.2 referenced |
| **Qwen Code** | 10 tracked; security discussion 8 comments | 10 PRs (multiple merged) | v0.22.0 (stable) + nightly |
| **DeepSeek TUI (CodeWhale)** | 2 issues | 7 PRs | v0.9.11 RC in preparation |

**Key observations:** Gemini CLI, OpenCode, Pi, and Qwen Code show the highest PR velocity. Claude Code and Copilot CLI are in consolidation phases with zero PR activity. DeepSeek TUI, while small, is actively preparing a new release.

---

## 3. Shared Feature Directions

| Direction | Tools | Specific Needs |
|---|---|---|
| **Multi-account / BYOK support** | Claude Code (#27302, #18435), Copilot CLI (#3282, #3709) | Profile switching, multiple models in one session, model picker parity with local/hosted providers |
| **Agent reliability & transparency** | Claude Code (claell cluster #85253–56), Gemini CLI (#22323 false GOAL success), Copilot CLI (#4566 no tool actions), Qwen Code (#9733 loop detection FPs) | Eliminate false success signals, reduce silent omissions, distinguish state-advancing loops from true loops |
| **Automatic model selection persistence** | Pi (#8376), Qwen Code (session model restoration), Copilot CLI (#3282) | Per-session/directory/global model preference persistence |
| **Memory & context management** | Kimi Code (#1283, #1478), OpenCode (#20695), Pi (#6879, #8464), Gemini CLI (#26522 low-signal retries) | Persistent cross-session memory, smarter compaction/detection, token-frugal reads |
| **Session reliability / audit trails** | Claude Code (#88383 empty thinking, #75037 lost records), Pi (#6879 context overflow), OpenCode (#43277 stuck sessions) | Crash-safe receipts, replayable session data, durability guarantees |
| **Sandboxing & security hardening** | Gemini CLI (Seatbelt PR), OpenCode (#2242), Qwen Code (#9556 code execution), Claude Code (#88896 hooks) | OS-level sandboxing, consent gates for env changes, deterministic tool-execution boundaries |
| **MCP ecosystem compatibility** | Copilot CLI (#4370 FastMCP), OpenCode (#40125 trust config), Gemini CLI (#28863 consent) | Graceful fallback for optional methods, per-server trust, fingerprint pinning |
| **Windows platform parity** | Claude Code (#88896 hooks), Copilot CLI (#4111 orphans), Pi (#8441, #8484), Codex (#39189 auth) | Fix path normalization, ConPTY rendering, process lifecycle, hook execution |

---

## 4. Differentiation Analysis

| Tool | Focus & Positioning | Target Users | Technical Approach |
|---|---|---|---|
| **Claude Code** | Enterprise-grade agent with governance hooks, session audit trails, and multi-account needs | Enterprise adopters, teams with compliance requirements | Connector-based OAuth, session JSONL, remote control, hooks system |
| **OpenAI Codex** | Alpha-fast iteration on thread attribution, guardian classifiers, runtime handoff | Developers integrating agent work into pipelines | Thread-source metadata, suspension mechanisms, CLI+SDK parity |
| **Gemini CLI** | Security-first with aggressive sandboxing; active security research community | Developers on macOS/Linux with container workflows | Seatbelt profiles, variable-expansion gates, consent prompts, A2A server |
| **Copilot CLI** | Tightly coupled to GitHub ecosystem; cloud workflows; enterprise auth | GitHub-centric teams, `--cloud` adopters | Copilot auth, remote sessions, BYOK via env vars, MCP integration |
| **Kimi Code** | Bilingual (CN/EN) with strong memory feature demand; plugin ecosystem forming | Developers in CN/Asia; large-project users | Plugin system, `StrReplaceFile` tooling, agent.md convention |
| **OpenCode** | Open model-agnostic TUI with heavy community engagement on memory/sandboxing | TUI enthusiasts, multi-provider users | SQLite sessions, Astro site, MCP trust config, per-MCP CA pinning |
| **Pi** | Cross-platform TUI with provider gateway model; strong Windows pain | Developers who want a full TUI with model flexibility | Rust TUI, ConPTY handling, bundled Node, provider ecosystem (MindsHub, Copilot) |
| **Qwen Code** | Review-loop tooling and code-review infrastructure; China ecosystem (DingTalk, Aone) | Teams running automated code review at scale | Content-anchored findings, execution-grade verification, worktree management |
| **DeepSeek TUI (CodeWhale)** | DeepSeek-specific TUI with crate decomposition; machine-readable supervision | DeepSeek API users, scriptable session workflows | Rust crate architecture, portable-pty, lifecycle outboxes, control sockets |

---

## 5. Community Momentum & Maturity

**Highest momentum (rapid iteration):**
- **Gemini CLI** — Multiple security-critical PRs merged in 24h; first-time contributor shipped a sandbox escape fix; active P1 triage cycles
- **OpenCode** — 5 merged PRs in 24h across core, TUI, and website; maintainers actively responding to memory megathread
- **Qwen Code** — Review-loop features shipping weekly; 20-round review PRs landing; substantial architectural hygiene work
- **Pi** — 6 merged/closed PRs in 24h including a high-impact ConPTY fix; Windows issues getting targeted attention

**Consolidation phase (stabilizing, lower PR velocity):**
- **Claude Code** — Maintenance release only; repository quiet; community demand concentrated on multi-account (1,105 combined upvotes) but no visible PR progress
- **Copilot CLI** — No PR activity; new triage issues piling up; community waiting on multi-model support

**Maturing but smaller communities:**
- **Kimi Code** — Smaller cycle; 1 merged critical fix (UTF-8 preservation); memory feature demand is vocal but not yet addressed
- **DeepSeek TUI** — Small but systematized via EPIC/FEAT structure; release hygiene is a focus

**Emerging communities with intensity:**
- **OpenCode** and **Pi** show unusually high engagement relative to their size, suggesting they serve a distinct niche (open-model TUI users, multi-provider enthusiasts) with strong loyalty.

---

## 6. Trend Signals

**For developers evaluating tools:**

1. **Agent reliability is the new frontier.** The most damaging issues across all tools are silent failures masked as success (`GOAL` status with no work done, agent acknowledges without executing, empty thinking blocks). Prioritize tools that expose execution traces, durable receipts, and verification evidence over those that only report outcomes.

2. **Multi-account and BYOK are table-stakes for adoption.** Claude Code's 1,105 combined upvotes and Copilot CLI's 53 reactions show this is not a niche request. Expect all major tools to ship profile switching within 2–3 quarters. Evaluate early whether your workflow needs identity isolation.

3. **Windows support remains the weakest link.** Pi's 6 separate Windows bugs in one week, Codex auth corruption, and Claude Code's hook failure reveal a consistent pattern: macOS is the first-class citizen. If your team is Windows-heavy, budget for environment-specific debugging or check feature parity explicitly.

4. **Security hardening is accelerating in response to real exploits.** Gemini CLI's sandbox escape fix, variable-expansion bypass patches, and consent-gate PRs represent a genuine shift toward treating agent sandboxes as attack surfaces. For production deployments, prioritize tools with active security-issue tracks.

5. **Memory management is the top reliability blocker.** OpenCode's memory megathread (135 comments), Pi's auto-compaction failure (2-hour session loss), Qwen's 1TB-server OOM, and Kimi's persistent-memory demand all point to context management as the differentiator between "demo-ready" and "production-ready." Ask every tool vendor about their compaction strategy and memory leak posture.

6. **Review-loop tooling is a rising specialization.** Qwen Code's execution-grade verification, convergence advisories, and content-anchored findings suggest that AI-assisted code review is becoming a competitive moat. If your team runs automated review pipelines, watch this space closely.

7. **Session auditability is becoming a compliance requirement.** Claude Code's thinking-block regression and background-agent record loss, plus OpenCode's stuck sessions, highlight that "what did the agent do" is becoming as important as "what did the agent produce." For regulated industries, demand session export, replay, and integrity guarantees.

---

*Report generated from public GitHub data for 9 AI CLI tools, snapshot 2026-08-23.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-08-23 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The following PRs have generated the most community discussion and represent the most significant activity in the repository.

### #1 — run_eval.py Fix (PR #1298)
**Status:** Open | **Author:** MartinCajiao | **Created:** 2026-06-10

This is one of the most critical fixes in the ecosystem. `run_eval.py` — the core evaluation script for Skill description optimization — reports `recall=0%` for every description, rendering the optimization loop useless. The PR addresses: installing the eval artifact as a real Skill, fixing Windows stream reading, trigger detection, and parallel worker issues. This fix is essential because multiple downstream tools (`run_loop.py`, `improve_description.py`) rely on this signal.

🔗 [View PR #1298](https://github.com/anthropics/skills/pull/1298)

---

### #2 — document-typography Skill (PR #514)
**Status:** Open | **Author:** PGTBoos | **Created:** 2026-03-04

A quality-control Skill that prevents common typographic problems in AI-generated documents: orphan word wrap (1-6 words spilling onto the next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment. Community discussion notes these issues affect virtually every document Claude generates, making this a universally applicable Skill with high adoption potential.

🔗 [View PR #514](https://github.com/anthropics/skills/pull/514)

---

### #3 — ODT Skill — OpenDocument Creation (PR #486)
**Status:** Open | **Author:** GitHubNewbie0 | **Created:** 2026-03-01

A comprehensive Skill for creating, filling, reading, and converting OpenDocument Format files (.odt, .ods). Triggers on mentions of 'ODT', 'ODS', 'ODF', 'OpenDocument', 'LibreOffice document', or open-source/ISO standard document requests. The community interest reflects growing demand for open-format document support alongside the existing docx/pdf skills.

🔗 [View PR #486](https://github.com/anthropics/skills/pull/486)

---

### #4 — frontend-design Clarity Improvement (PR #210)
**Status:** Open | **Author:** justinwetch | **Created:** 2026-01-05

A revision of the frontend-design Skill to improve clarity, actionability, and internal coherence. The goal is ensuring every instruction is something Claude can actually follow within a single conversation, with guidance specific enough to steer behavior without being overly prescriptive. This is a hot topic as the community focuses on Skill quality optimization.

🔗 [View PR #210](https://github.com/anthropics/skills/pull/210)

---

### #5 — Skill Quality & Security Analyzers (PR #83)
**Status:** Open | **Author:** eovidiu | **Created:** 2025-11-06

Adds two meta-skills to the `example-skills` collection: **skill-quality-analyzer** (evaluates Structure & Documentation, examples, resources across five weighted dimensions) and **skill-security-analyzer**. These address the community's growing concern about Skill reliability and security — responding directly to the trust-boundary issues raised in Issue #492.

🔗 [View PR #83](https://github.com/anthropics/skills/pull/83)

---

### #6 — PDF Case-Sensitivity Fix (PR #538)
**Status:** Open | **Author:** Lubrsy706 | **Created:** 2026-03-06

Fixes 8 case-sensitivity mismatches in the PDF Skill's `SKILL.md` — `REFERENCE.md` → `reference.md` (4 occurrences) and `FORMS.md` → `forms.md` (4 occurrences). This breaks on case-sensitive filesystems (Linux/macOS). While simple, it highlights the cross-platform stability concerns gaining attention in the community.

🔗 [View PR #538](https://github.com/anthropics/skills/pull/538)

---

### #7 — ServiceNow Platform Skill (PR #568)
**Status:** Open | **Author:** Vanka07 | **Created:** 2026-03-08

A broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD/CSM, SPM/PPM, Vulnerability Response, and Security Incident Response. The scope is intentionally broader than a narrow scripting helper, positioning this as an enterprise-grade Skill. Despite complexity concerns, it represents a significant enterprise platform integration demand.

🔗 [View PR #568](https://github.com/anthropics/skills/pull/568)

---

### #8 — Pyxel Retro Game Development (PR #525)
**Status:** Open | **Author:** kitao | **Created:** 2026-03-05

A Skill for [pyxel-mcp](https://github.com/kitao/pyxel-mcp), an MCP server for the Pyxel retro game engine. Triggers when users want to create retro/pixel-art/8-bit games with Python. Covers the full workflow: write → run_and_capture → inspect → iterate. Shows the community's interest in creative/entertainment-focused Skills.

🔗 [View PR #525](https://github.com/anthropics/skills/pull/525)

---

## 2. Community Demand Trends

**Tier 1 — Security & Trust (Critical):** Issue #492 (43 comments) is the community's loudest concern. Community-made Skills distributed under the `anthropic/` namespace create a trust boundary vulnerability. Users may grant elevated permissions to community Skills they believe are official. This has concrete demands: explicit community-contribution labels, namespace segregation, and permission guidance.

**Tier 2 — Reliability Infrastructure:** Issues #556 (run_eval.py 0% trigger rate, 12 comments) and #202 (skill-creator needs best-practice updates, 8 comments) reveal the community's focus on making the Skill-creation toolchain itself reliable and Standards-compliant.

**Tier 3 — Enterprise Features:** Issue #228 (16 comments) requests org-wide skill sharing in Claude.ai — currently users must manually send .skill files via Slack/Teams and have colleagues upload them. This is the clearest enterprise adoption signal.

**Tier 4 — Document/Format Coverage:** Issues #12 (docx whitespace corruption), #1175 (SharePoint Online security concerns), and PRs for ODT/PDF demonstrate sustained demand for robust document format handling with emphasis on file integrity.

**Tier 5 — Context-Window Awareness:** Issue #1487 (claude-api Skill injecting ~156k tokens, exhausting context) shows the community is hitting real limits and demanding Skills that are context-efficient.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and may land soon:

### self-audit Skill (PR #1367)
**Author:** YuhaoLin2005 | **Created:** 2026-06-28 | **Last updated:** 2026-07-02

A skill that audits AI output before delivery — mechanical file verification first, then a four-dimension reasoning audit in damage-severity priority order. Claims to be universal across any project, tech stack, or model. Backed by a detailed proposal in Issue #1385.

🔗 [View PR #1367](https://github.com/anthropics/skills/pull/1367)

---

### testing-patterns Skill (PR #723)
**Author:** 4444J99 | **Created:** 2026-03-22 | **Last updated:** 2026-04-21

A comprehensive testing Skill covering the Testing Trophy model, what to test vs. what NOT to test, AAA pattern, React component testing with Testing Library, and edge cases. Addresses the testing-generation gap in the current Skills collection.

🔗 [View PR #723](https://github.com/anthropics/skills/pull/723)

---

### skill-creator Windows Fixes (PR #1099 & PR #1050)
**Authors:** joshuawowk, gstreet-ops | **Created:** 2026-04-27 to 2026-05-07

Two related PRs fixing Windows-specific issues in the skill-creator tooling: `run_eval.py` crashes with `[WinError 10038]` reading from subprocess pipes (PR #1099) and `subprocess.Popen(["claude", ...])` fails with `[WinError 2]` because Windows ships the CLI as `claude.cmd` and Python doesn't honor `PATHEXT` (PR #1050). These are essential for Windows users but appear to be converging — possible consolidation ahead.

🔗 [View PR #1099](https://github.com/anthropics/skills/pull/1099) | [View PR #1050](https://github.com/anthropics/skills/pull/1050)

---

### CONTRIBUTING.md (PR #509)
**Author:** narenkatakam | **Created:** 2026-03-03

Adds a `CONTRIBUTING.md` to improve the repo's GitHub community health score (currently 25%). Includes five sections covering the contribution lifecycle. This is an infrastructure improvement, but directly enables higher-quality community contributions going forward.

🔗 [View PR #509](https://github.com/anthropics/skills/pull/509)

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, secure, and professional-grade Skills development pipeline** — specifically fixing the broken `run_eval.py` evaluation tooling, securing the trust boundary around community Skills distribution, and adding enterprise-ready Skills (org sharing, ServiceNow, compliance-oriented analysis) rather than purely creative or niche examples.

---

*Report generated from public GitHub activity on anthropics/skills as of 2026-08-23.*

---

# Claude Code Community Digest — 2026-08-23

## Today's Highlights

A quiet release day with v2.1.240 shipping incremental reliability fixes. Community attention remains heavily focused on multi-account authentication support (#27302, #18435) — the two most-commented issues in the tracker with a combined 402 comments and 1,105 upvotes. A new cluster of model-behavior reports from claell (#85253–#85256) surfaced concerns about hallucinated confidence and silent task omission, signaling growing scrutiny of agent reliability in production use.

## Releases

**v2.1.240** — Bug fixes and reliability improvements. No additional details provided in the changelog.

## Hot Issues

1. **[#27302 — Support multiple Connector accounts (same connector, different accounts)**](https://github.com/anthropics/claude-code/issues/27302) — The second most-upvoted open issue (357 👍, 234 comments). Users need to maintain distinct identity contexts (e.g., personal vs. work) through the same OAuth connector. High engagement indicates this is a core workflow blocker for enterprise adopters.

2. **[#18435 — Manage multiple Claude accounts with easy profile switching in Desktop**](https://github.com/anthropics/claude-code/issues/18435) — The most-upvoted issue overall (748 👍, 168 comments). Complements #27302 but focuses on the Desktop app experience. Together these represent the single strongest feature demand in the tracker.

3. **[#88383 — 2.1.238 regression: thinking blocks persist as empty signature-only husks**](https://github.com/anthropics/claude-code/issues/88383) — A regression where interactive sessions record `{"type": "thinking", "thinking": "", "signature": "<sig>"}` in session JSONL. Breaks session replay and audit trails — a data-integrity issue that matters for teams relying on session history.

4. **[#51267 — Remote Control: session hangs mid-execution with no remote unstick mechanism**](https://github.com/anthropics/claude-code/issues/51267) — Mobile remote control sessions silently hang; only a local Esc recovers. 17 comments suggest multiple users have hit this. Critical "day 2" issue for remote-first workflows.

5. **[#62202 — SIGTERM exits every exactly 5 minutes in Desktop & VS Code extension**](https://github.com/anthropics/claude-code/issues/62202) — A 300-second kill interval that affects Desktop and VS Code wrappers but not terminal CLI. Points to a watchdog timer bug rather than resource pressure; severe for any extended session.

6. **[#85253–#85256 — Model behavior cluster: fabricated confidence, omitted work**](https://github.com/anthropics/claude-code/issues/85253) — Four issues by claell documenting: claims presented as facts when inferred, silent omission of multi-part request items, private drafting leaking into public output, and delegated tasks being expanded into self-authored work. These are the kind of trust-eroding behaviors that matter most for production autonomy.

7. **[#87947-related — Interactive sessions vs. sdk-cli print mode thinking persistence**](https://github.com/anthropics/claude-code/issues/88383) — Linked from #88383, this documents the same copy for SDK/print mode. The pair suggests a systemic issue in how thinking blocks are serialized across entrypoints.

8. **[#75037 — Background agents: fast termination, crash-loop on attach, lost completion records**](https://github.com/anthropics/claude-code/issues/75037) — Three failure modes in `claude --bg` workflows. Losing completion records is the most damaging: agents do real work that vanishes from the audit trail.

9. **[#88896 — PreToolUse hooks never fire on Windows (v2.1.240)**](https://github.com/anthropics/claude-code/issues/88896) — Core governance hooks are silently bypassed on Windows. For any team with compliance or safety hooks, this is a critical security-relevant bug.

10. **[#88884 — `--agent` flag triggers full onboarding on every Docker restart**](https://github.com/anthropics/claude-code/issues/88884) — A 9-step onboarding loop in containerized environments. Blocking for any CI/CD or container-native usage — a significant deployment friction point.

## Key PR Progress

No PRs were merged or updated in the past 24 hours. The repository is likely in a stabilization phase following the v2.1.240 patch release. The absence of open PR activity combined with a maintenance release suggests the team is consolidating rather than shipping new surface area.

## Feature Request Trends

1. **Multi-account architecture** — The dominant theme (#27302, #18435). Users need: (a) multiple accounts through one connector, (b) profile switching in Desktop, and (c) isolation of sessions by identity. This is a platform-level requirement for serious multi-tenant usage.

2. **Agent session management** — #88907 asks for active-first sorting of agents in the panel; #75037 highlights failures in background agent workflows. The trend is toward "fleets of agents you can observe and control," not single-session interactions.

3. **UI/UX polish for long-running sessions** — Dark-mode text-selection contrast (#81919), muted auto-update banners (#88858), and voice dictation code-switching (#83881) all indicate the community considers the feature set mature and is now asking for fit-and-finish in daily workflows.

4. **Reduced onboarding friction for containers/CI** — #88884 (Docker onboarding loop) and the general direction of "headless-friendly" features point to a demand for zero-interaction setup in automated environments.

## Developer Pain Points

- **Intermittent agent reliability**: The claell cluster (#85253–#85256) and #77745 paint a picture of an agent that overstates certainty and silently drops work. For developers delegating real tasks, this is the difference between a useful tool and a liability.

- **Session data integrity**: Empty thinking blocks (#88383) and lost background-agent completion records (#75037) break the audit trail that teams rely on for trust. "Did it happen" questions are harder to answer than "did it work."

- **Platform gaps on Windows and Linux**: PreToolUse hooks not firing on Windows (#88896) and desktop-process SIGTERM kills (#62202) show that cross-platform behavior lags the macOS experience. Developers on non-macOS platforms are spending time on environment-specific debugging.

- **Silent failures in wrappers**: The 5-minute SIGTERM (#62202) and mobile queue discard (#85924) share a pattern — the system fails without surfacing an error, leaving users to discover corrupted state later.

- **Connector/account management friction**: With 1,105 combined upvotes across the two multi-account issues, this is the clearest sustained pain point. Developers are juggling work and personal identities and cannot cleanly separate them in Claude Code today.

---

*Data source: github.com/anthropics/claude-code — snapshot for 2026-08-23*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-23

## Today's Highlights

Two alpha releases (`rust-v0.150.0-alpha.7` and `rust-v0.149.0-alpha.7.2`) landed in the last 24 hours. The most significant PR activity centers on thread-source attribution for `codex exec` calls, enabling integrations to classify agent-initiated work, plus a new thread-suspension mechanism for safer runtime recovery. The community continues to be most vocal about rate-limit drain rates, macOS resource runaway, and recurring auth/401 issues across platforms.

---

## Releases

| Version | Notes |
|---|---|
| **rust-v0.150.0-alpha.7** | Rolling alpha release — no detailed changelog published. |
| **rust-v0.149.0-alpha.7.2** | Patch alpha release — no detailed changelog published. |

This is a pre-release track; expect the next stable bump to consolidate these alpha changes.

---

## Hot Issues

**1. [macOS] Codex Desktop triggers `syspolicyd` / `trustd` CPU/memory runaway**  
→ #25719 · 394 👍 / 85 comments  
The highest-reaction issue this week. Desktop repeatedly triggers macOS security daemons, causing sustained resource exhaustion. Community is asking for a quarantine/notarization fix.  
Link: https://github.com/openai/codex/issues/25719

**2. Weekly limit draining like the old 5-hour limit**  
→ #33685 · 15 👍 / 28 comments  
Users report the new weekly limit burns at roughly the same rate as the old 5-hour cap, despite model selection not changing. Strong sentiment that the limit system is misconfigured or overly aggressive.  
Link: https://github.com/openai/codex/issues/33685

**3. Custom pets fail to load in WSL due to path normalization**  
→ #20730 · 28 👍 / 23 comments  
Persistent WSL path-mapping problem; pets directory under Windows/WSL hybrid setups isn't resolved. Long-running (since May) and still unimplemented.  
Link: https://github.com/openai/codex/issues/20730

**4. [Windows] Opening existing thread signs out personal Pro account after workspace-only 401**  
→ #39189 · 4 👍 / 17 comments  
Auth state corruption on Windows; a 401 from workspace-only settings triggers full sign-out. High-impact for Pro users on Windows.  
Link: https://github.com/openai/codex/issues/39189

**5. AWS Bedrock GPT-5.6 Sol — no explicit cache controls, high cache-write spend**  
→ #37674 · 12 👍 / 13 comments (CLOSED)  
Production cost evidence that the CLI cannot emit `prompt_cache_breakpoint` for Bedrock Mantle, leading to inflated cache-write token charges. Closed, presumably with a fix tracked elsewhere.  
Link: https://github.com/openai/codex/issues/37674

**6. Weekly usage reset date changed after subscribing to ChatGPT Plus**  
→ #30816 · 4 👍 / 11 comments  
Users report unexpected reset-date shifts on plan change; unclear billing-cycle logic.  
Link: https://github.com/openai/codex/issues/30816

**7. Pro account: 5-hour usage bucket disappeared from API and App**  
→ #32707 · 3 👍 / 10 comments  
Parallels #33685 — the removal of the 5-hour bucket from `account/rateLimits/read` caused confusion about which limit is being consumed.  
Link: https://github.com/openai/codex/issues/32707

**8. Background exec deletes `~/.codex/skills/.system`**  
→ #19265 · 6 👍 / 10 comments  
Intermittent deletion of system skills directory on Desktop, breaking bundled skills like `imagegen` and `openai-*`.  
Link: https://github.com/openai/codex/issues/19265

**9. Windows sandbox setup helper fails with 0xc0000142 only when launched by Codex**  
→ #34928 · 0 👍 / 2 comments  
Repro-able but low-traffic; UAC flow works but the sandbox helper crashes when Codex launches it.  
Link: https://github.com/openai/codex/issues/34928

**10. False-positive usage-policy violations mid-session (GPT-5.6 Sol)**  
→ #39745 · 0 👍 / 2 comments  
Innocent sessions randomly start complaining about policy violations even halfway through. Enterprise users affected; suggests classifier mis-firing.  
Link: https://github.com/openai/codex/issues/39745

---

## Key PR Progress

**1. #40161 — Allow exec callers to classify new threads**  
Adds global `codex exec --thread-source` and propagates it to forked threads; defaults to `user`.  
https://github.com/openai/codex/pull/40161

**2. #40155 — exec: expose thread source in CLI and TypeScript SDK**  
Companion to #40161; lets integrations attribute agent work to the initiating feature.  
https://github.com/openai/codex/pull/40155

**3. #40150 — Use thread source metadata for Guardian classifiers**  
Replaces `request_kind`/`is_guardian_mode` with `thread_source: guardian_classifier` metadata; updates sampler and tests.  
https://github.com/openai/codex/pull/40150

**4. #40068 — Report runtime MCP connection status**  
Adds nullable `runtimeStatus` to `mcpServerStatus/list` for thread-scoped connections.  
https://github.com/openai/codex/pull/40068

**5. #40038 — Add unfinished root turn suspension**  
New `CodexThread::suspend_turn_and_shutdown` and `SuspendTurnOutcome` to stop an active root turn without marking complete/aborted, enabling runtime handoff.  
https://github.com/openai/codex/pull/40038

---

## Feature Request Trends

1. **Thread-source attribution for agent work** — Multiple PRs (#40155, #40161, #40150) indicate the team is actively standardizing how threads are classified (user vs. agent/guardian), enabling better metering and auditing.
2. **Session transfer between CLI and Desktop** — #40055 (closed as enhancement) requests that CLI sessions appear as Codex sessions (not generic Work chats) in Desktop history; community interest in full cross-surface continuity.
3. **Explicit prompt-cache controls** — #35300 and #37674 both push for CLI-level `prompt_cache_breakpoint` emission for GPT-5.6 Sol to control cost on long-running agentic loops.
4. **MCP runtime status surfacing** — #40068 points toward making MCP connection state visible in inventory, not just tool availability.

---

## Developer Pain Points

- **Rate-limit opacity and unbounded drain** — The weekly limit (and the vanished 5-hour bucket) is the single largest recurring complaint; users can't predict when they'll get cut off.
- **Auth instability across platforms** — Windows 401-triggered sign-outs (#39189), repeated sign-in screens on macOS (#39803), and VSCode extension 401s (#40073) point to flaky token/session handling.
- **WSL path normalization breaks features** — Custom pets (#20730) and inline Visualize (#40100) both fail in WSL because `/mnt/c/...` paths are misnormalized.
- **False-positive policy violations** — Mid-session usage-policy errors (#39745) erode trust in the safety pipeline and interrupt legitimate work.
- **Silent resource leaks** — macOS `syspolicyd`/`trustd` runaway (#25719) and background skill-directory deletion (#19265) continue to be unresolved, high-reaction bugs.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-23

## Today's Highlights
A new nightly release hardens macOS sandboxing against container-runtime escapes, closing a significant security gap for Docker Desktop users. The community continues to push on agent reliability—particularly subagent turn-limit handling, shell hangs, and browser agent robustness—while maintainers review a wave of security-focused PRs addressing variable expansion bypasses and extension consent gaps.

## Releases
**v0.56.0-nightly.20260822.g5411f113c** — Fixes sandbox isolation on macOS Seatbelt profiles by denying access to Docker and container runtime daemon UNIX domain sockets, CLI binaries, Mach/XPC service lookups, and POSIX shared memory. This prevents sandbox escape via container hypervisor filesystem mounts (e.g., Docker Desktop VirtioFS). Contributed by first-time contributor @josebalius ([PR #28935](https://github.com/google-gemini/gemini-cli/pull/28935)).

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 13 comments, 2 👍)  
   The `codebase_investigator` subagent reports `success` with `Termination Reason: "GOAL"` even when it hit the max turn limit without doing any analysis. This masks real interruptions and produces misleading results. Active retesting ongoing.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8 comments, 8 👍)  
   High community impact: any deferral to the generalist agent hangs indefinitely (up to an hour). Workaround: explicitly instructing the model not to use subagents. Strong 👍 count signals broad frustration.

3. **[#25166 — Shell command stuck on "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 3 👍)  
   Simple CLI commands hang after finishing, showing "Awaiting user input." Highly disruptive to automation workflows and recurring for the reporter.

4. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, 4 comments, 1 👍)  
   Browser agent terminates with `GOAL` status but fails immediately on Wayland sessions. Linux desktop users are impacted; needs retesting.

5. **[#22186 — get-shit-done output hook crashes CLI](https://github.com/google-gemini/gemini-cli/issues/22186)** (P1, 3 comments)  
   Crash occurs when the output hook is "almost finished printing user summary." Reproducible and blocks a popular workflow.

6. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments)  
   Sessions deemed "low-signal" by the extraction agent remain unprocessed and keep surfacing. Inefficient and wasteful of tokens/compute.

7. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 4 comments)  
   Security concern: transcripts are sent to the model *before* redaction happens, and secrets can be logged. Privacy-sensitive feature needs hardening.

8. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments)  
   Anecdotal but recurring: custom skills and sub-agents are ignored unless explicitly instructed. Users want more autonomous adoption of configured skills.

9. **[#24246 — 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, 3 comments)  
   Tool count exceeds API limits, causing hard failures. Users expect smarter tool scoping rather than a blanket limit.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, 3 comments, 1 👍)  
   Model uses `git reset --force` and other destructive commands when safer alternatives exist. Safety-critical UX concern for production users.

## Key PR Progress

1. **[#28902 — Block $VAR and ${VAR} variable expansion bypass (GHSA-wpqr-6v78-jr5g)](https://github.com/google-gemini/gemini-cli/pull/28902)** (P1, security)  
   Fixes an incomplete check in bash/PowerShell substitution detection that allowed variable expansion patterns to bypass the security gate. Includes defense-in-depth hardening of CI workflow.

2. **[#28935 — Isolate Docker/container runtime sockets and binaries in macOS Seatbelt](https://github.com/google-gemini/gemini-cli/pull/28935)** (merged into nightly)  
   Denies access to container runtime daemon sockets, CLI binaries, XPC service lookups, and POSIX shared memory. Prevents sandbox escapes via Docker Desktop VirtioFS mounts.

3. **[#28863 — Prompt for consent on environment changes and sanitize runtime-altering env vars](https://github.com/google-gemini/gemini-cli/pull/28863)** (security)  
   Prevents extension updates from bypassing consent checks and injecting unauthorized environment variables into MCP server processes. Closes a significant supply-chain gap.

4. **[#28967 — Prevent clearing terminal scrollback on static refresh](https://github.com/google-gemini/gemini-cli/pull/28967)** (P2, core)  
   Fixes `refreshStatic()` calling `clearTerminal` which wiped scrollback on Linux/Unix terminals. Improves terminal UX for non-alternate-buffer mode.

5. **[#28968 — Dedupe symlinked/junctioned skills directories during discovery](https://github.com/google-gemini/gemini-cli/pull/28968)** (P3, extensions)  
   When `.gemini` is a Windows junction/symlink to `.agents`, CLI scanned both paths as if separate. Fixes double-scanning and duplicate skill definitions.

6. **[#28940 — Clear stale cancellation error on new message turns (A2A server)](https://github.com/google-gemini/gemini-cli/pull/28940)** (core)  
   Fixes state corruption where subsequent user prompts crash with `Execution aborted` after a cancellation. Resolves the "Google Cloud Assistant execution stopped" issue.

7. **[#28961 — Declare top-level safety checkers in write policy configuration](https://github.com/google-gemini/gemini-cli/pull/28961)** (policy)  
   Realigns safety checker definitions to standard `[[safety_checker]]` table arrays, ensuring `AllowedPathChecker` is properly registered for `write_file` and `replace` tools.

8. **[#27862 — Preserve executing subagent tool calls in UI](https://github.com/google-gemini/gemini-cli/pull/27862)** (P2, CLI)  
   Fixes subagent tool calls disappearing from the UI while still active in `useToolScheduler`. Improves visibility into ongoing subagent work.

9. **[#28963 / #28966 — Correct excludeTools docs that never match](https://github.com/google-gemini/gemini-cli/pull/28963)** (P1, docs)  
   Documentation told users to write `"run_shell_command(rm -rf *)"` in `excludeTools`, but matching is by exact tool name—so nothing was excluded. Both PRs correct docs and point to the policy engine for command-level blocking.

10. **[#28892 — Preserve empty text turns with tools or media](https://github.com/google-gemini/gemini-cli/pull/28892)** (core, closed)  
    Refines chat history validation so model turns with empty text parts are preserved when they carry tool requests/responses or multimodal media. Prevents data loss in curated history.

## Feature Request Trends

- **AST-aware codebase tooling** ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)): Community is pushing for AST-aware file reads, method-boundary slicing, and codebase mapping to reduce token bloat and improve navigation precision.
- **Subagent introspection & transparency** ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763), [#22598](https://github.com/google-gemini/gemini-cli/issues/22598)): Users repeatedly request subagent context in `/bug` reports and visible/shared trajectories via `/chat share`.
- **Persistent file-based task tracking** ([#18836](https://github.com/google-gemini/gemini-cli/issues/18836), [#21000](https://github.com/google-gemini/gemini-cli/issues/21000)): Replace in-context `WriteToDo` with CRUD-backed persistent tracking to fight context rot and cross-session memory loss.
- **Tactful extraction / token-frugal reads** ([#19561](https://github.com/google-gemini/gemini-cli/issues/19561)): A prioritized hierarchy (grep → surgical read → full read) to keep context below a ~36.6k token baseline.
- **Self-aware agent** ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)): Agent should know its own CLI flags, hotkeys, and self-execution capabilities to act as its own expert guide.

## Developer Pain Points

- **Hangs and stalls are the #1 pain**: Generalist agent hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell commands stuck on "Waiting input" ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and interactive prompts blocking Vite scaffolding ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)) are top-voted frustrations.
- **False success signals**: MAX_TURNS reported as GOAL success ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) and browser failures masked as success undermine trust in automation.
- **Tool/skill discoverability & adoption**: Skills and sub-agents are ignored unless forced ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)); tool limits cause 400 errors ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)).
- **Destructive commands**: The model occasionally uses `git reset --force` or similar destructive operations when safer alternatives exist ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).
- **Sandbox escape vectors**: The new Seatbelt fix ([#28935](https://github.com/google-gemini/gemini-cli/pull/28935)) and variable expansion bypass ([#28902](https://github.com/google-gemini/gemini-cli/pull/28902)) show active security research; users should update promptly.
- **Auto Memory privacy/efficiency**: Transcripts sent before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) and infinite low-signal retries ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)) are unresolved friction points.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**2026-08-23**

---

## 1. Today's Highlights
No new releases or merged PRs landed in the last 24 hours, but the issue tracker remains active with ten items receiving updates. The community is increasingly vocal about **multi-model support**—particularly the ability to switch between BYOK/local providers and GitHub-hosted models within a single session (issues #3282 and #3709 together have accumulated 53 reactions). Two new triage-stage issues report concerning stability problems: an agent loop where Copilot acknowledges work without executing tool actions (#4566), and a multi-symptom `--cloud` failure including hangs and 429 rate limiting (#4568).

---

## 2. Releases
No new releases in the last 24 hours.

---

## 3. Hot Issues

### Multi-Model & BYOK Support (High Demand)
- **[#3282 — Add multiple BYOK model capability in copilot CLI](https://github.com/github/copilot-cli/issues/3282)** — [OPEN] [area:models, area:configuration] — 26 👍, 9 comments
  Users want to configure multiple BYOK models (via env vars or config) and switch between them inside the TUI without restarting the session. Currently, only a single model is supported via `COPILOT_MODEL`. The 26 upvotes signal strong community interest in flexible model configuration.

- **[#3709 — Allow /model to switch between multiple models including BYOK/local providers in one session](https://github.com/github/copilot-cli/issues/3709)** — [OPEN] [area:models] — 27 👍, 5 comments
  The `/model` picker only lists GitHub-hosted models, omitting configured BYOK providers. Users want a unified model picker that includes local/self-hosted models. This is the most-upvoted open issue this week, indicating a top-priority feature request.

### Authentication & Enterprise
- **[#2306 — "You are not authorized" error intermittently for enterprise users](https://github.com/github/copilot-cli/issues/2306)** — [OPEN] [area:authentication, area:enterprise] — 3 👍, 7 comments
  Enterprise users report intermittent authorization failures ("requires an enterprise or organization policy to be enabled") that appear 2–3 times a week and then vanish. The inconsistency is frustrating and disrupts workflow, with no clear root cause or workaround yet.

### MCP (Model Context Protocol) Stability
- **[#4370 — MCP initialization fails when `server/discover` returns `-32602`](https://github.com/github/copilot-cli/issues/4370)** — [OPEN] [area:mcp] — 1 👍, 2 comments
  Copilot CLI 1.0.79-1 cannot connect to FastMCP servers because the CLI sends a `server/discover` request that FastMCP doesn't implement, returning `-32602 Invalid request parameters`. Copilot treats this as a fatal failure instead of gracefully falling back. This breaks compatibility with a popular MCP framework.

### Session Management
- **[#4514 — Unable to restore remote session locally](https://github.com/github/copilot-cli/issues/4514)** — [OPEN] [area:sessions] — 1 👍, 1 comment
  Using `/resume` to restore a remote session locally fails with an unclear error. Users expect session portability across environments—a key workflow for developers who switch between local and cloud.

- **[#4111 — Windows: orphaned processes after auto-update spin at 100% CPU](https://github.com/github/copilot-cli/issues/4111)** — [OPEN] [area:sessions, area:platform-windows, area:installation] — 0 👍, 1 comment
  On Windows, long-running sessions kept alive across an in-place auto-update continue executing from the renamed `copilot.exe.old` binary instead of exiting. A large fraction of these orphaned processes spin one thread at 100% CPU indefinitely, causing system resource drain.

### New Triage Issues (August 22)
- **[#4566 — Agent repeatedly acknowledges work without executing tool actions](https://github.com/github/copilot-cli/issues/4566)** — [OPEN] [triage] — 0 👍, 1 comment
  With `gpt-5.3-codex` on v1.0.80, the agent verbally acknowledges a request but never invokes any tool actions, creating an infinite loop of non-productive responses. This is a critical usability bug that undermines trust in the agent.

- **[#4568 — `--cloud` owner picker hangs, reconnect crashes, task polling reaches 429](https://github.com/github/copilot-cli/issues/4568)** — [OPEN] [triage] — 0 👍, 0 comments
  Three interconnected failures in `copilot --cloud`: hangs at "Loading available owners..." without repo context, cloud tasks stuck at `session.requested` until timeout, and aggressive polling causing 429 rate limits. This is a multi-faceted stability issue for cloud workflows.

- **[#4567 — Opt-in for insecure (http://) OTLP exporter endpoint](https://github.com/github/copilot-cli/issues/4567)** — [OPEN] [triage] — 0 👍, 0 comments
  When using an OTLP/HTTP exporter with an `http://` endpoint (e.g., local loopback collector at `localhost:4318`), the CLI silently disables telemetry export. Users want an explicit opt-in to trust insecure endpoints, aligning with VS Code's behavior.

- **[#4565 — App Configuration Problems in repo `copilot-runtime-bazel-cache`](https://github.com/github/copilot-cli/issues/4565)** — [OPEN] [triage] — 0 👍, 0 comments
  Automated scanner (hubot) reports configuration issues that may cause "unexpected application behavior" in a related repository. Likely a maintenance/ops item rather than a user-facing bug.

---

## 4. Key PR Progress
No pull requests were updated in the last 24 hours. The repository is in a quiet phase for code changes, with discussion concentrated on the issues above.

---

## 5. Feature Request Trends

| Trend | Description | Representative Issues |
|---|---|---|
| **Multi-model flexibility** | The dominant request: support multiple BYOK models, local providers, and in-session model switching via `/model`. Users want parity between local and GitHub-hosted models. | #3282, #3709 |
| **Observability alignment** | Opt-in to trust insecure OTLP endpoints (e.g., local collectors) instead of silently disabling telemetry. Users expect parity with VS Code's telemetry settings. | #4567 |
| **Session portability** | Restore remote sessions locally without friction; persist model selections across sessions. | #4514, #3282 |
| **MCP ecosystem compatibility** | Graceful handling of MCP servers that don't implement optional methods like `server/discover`, allowing broader MCP server compatibility. | #4370 |

---

## 6. Developer Pain Points

1. **Model switching frustration** — The `COPILOT_MODEL` env var pins a session to a single model; users must terminate and restart to change models. Combining this with BYOK providers that aren't shown in the `/model` picker forces awkward workarounds. (26-27 upvotes each; **highest community engagement this week**)

2. **Intermittent enterprise auth failures** — The "requires an enterprise or organization policy" error appears randomly, disrupts work, then disappears without explanation. Hard to debug without a consistent repro. (7 comments, ongoing since March)

3. **MCP server incompatibility** — FastMCP servers are a popular choice; the CLI's strict handling of `server/discover` failures breaks integration entirely. Developers expect fallback or negotiation rather than hard failure.

4. **Windows auto-update process leaks** — Orphaned `copilot.exe.old` processes consuming 100% CPU indefinitely after updates is a resource leak that can degrade system performance, particularly for users who keep long-lived sessions.

5. **Cloud workflow instability** — The `--cloud` path has multiple failure modes (hang, timeout, 429s). This affects teams adopting remote/cloud execution and erodes confidence in the feature.

6. **Agent reliability concerns** — A new triage issue reports the agent "agreeing" to work but never executing tool actions. For an agentic CLI, silent non-action is a significant trust breaker.

---

*Sources: [github/copilot-cli issues](https://github.com/github/copilot-cli/issues), data retrieved 2026-08-23.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-23

## Today's Highlights
No new releases shipped in the last 24 hours, but the community's long-running call for a **persistent memory system** (#1283, #1478) continues to dominate discussion as the most-requested feature. Meanwhile, a **documentation PR for plugin security** (#2614) and a **critical UTF-8 corruption fix** (#2594, merged) represent the most substantive code movement this cycle.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

**#1283 — [enhancement] Feature Request: Memory System - Persistent context across sessions**  
*Author: CatKang | Updated: 2026-08-22 | Comments: 40*  
The flagship feature request. Proposes a dual-layer memory (AI-managed automatic notes + user-defined manual instructions) to persist project patterns and preferences across sessions. 40 comments make this the most-discussed issue, reflecting strong demand for long-horizon context in large codebases.  
[GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1283)

**#1478 — [enhancement] 能否优化记忆层？ (Can the memory layer be optimized?)**  
*Author: hahy36 | Updated: 2026-08-22 | Comments: 3*  
Bilingual frustration about the lack of documented memory features (only `agent.md` found), citing `.openclaw`'s SOUL.md/USER.md/MEMORY.md structure as a reference. Highlights that large-project usage is "painful" without persistent memory — a direct echo of #1283.  
[GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1478)

**#760 — [CLOSED] SSL certificate verification fails behind corporate proxy (Zscaler)**  
*Author: aaraujodata | Updated: 2026-08-22 | Comments: 3*  
Login fails with `SSLCertVerificationError` behind Zscaler proxies. Though closed, its continued updates suggest lingering interest in enterprise proxy support and custom CA trust configuration.  
[GitHub](https://github.com/MoonshotAI/kimi-cli/issues/760)

**#1478 / #1283 trend note:** Both memory-related issues were updated within the last 24h of this digest window, signaling that this remains an **unresolved, high-priority community pain point** rather than a settled discussion.

---

## Key PR Progress

**#2614 — [OPEN] docs(plugins): document security and persistent data**  
*Author: QIANLING-0831 | Updated: 2026-08-22*  
Scoped documentation-only PR clarifying the plugin contract: `plugin.json`, command-based tools, `inject`, and installation under `~/.kimi/plugins/`. Explicitly avoids describing separate plugin systems. Addresses a gap in plugin security and persistence documentation.  
[GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2614)

**#2594 — [CLOSED] fix(tools): preserve non-UTF-8 bytes in StrReplaceFile edits**  
*Author: 686f6c61 | Updated: 2026-08-22*  
Critical bug fix: `StrReplaceFile` previously decoded files with `errors="replace"`, corrupting any non-UTF-8 byte outside the edit region into `U+FFFD` (EF BF BD) on re-encode. Now applies edits as UTF-8 byte substrings on the raw buffer, preventing permanent data corruption. A must-merge for anyone using binary or legacy-encoded files.  
[GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2594)

---

## Feature Request Trends

1. **Persistent Memory System (dominant trend)** — Two issues (#1283, #1478) drive this direction: automatic AI-managed context + user-defined persistent instructions, with references to competitor patterns (`.openclaw`). Demand is driven by pain managing large, multi-session projects.
2. **Enterprise Proxy / TLS Support** — Despite closure, #760 keeps resurfacing, indicating ongoing demand for corporate-friendly SSL configuration (custom CAs, Zscaler-style interception).
3. **Documentation Completeness** — Both the memory and plugin topics show users struggling to find authoritative docs, pointing to a broader need for expanded reference material.

---

## Developer Pain Points

- **Loss of context across sessions** is the #1 recurring complaint — users explicitly state "painful when working on big projects" without memory persistence.
- **Inadequate documentation** around memory features and plugin internals forces users to reverse-engineer behavior or seek third-party references.
- **Enterprise environment friction** (SSL/proxy) remains a stumbling block for adoption in corporate settings, even if the specific issue is old.
- **Data integrity risks** — the UTF-8 corruption fix (#2594) underscores that tooling must be safe for non-UTF-8 files, a silent danger for mixed-encoding codebases.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-23

## Today's Highlights

The project saw a significant infrastructure push, with the website rebuilt on Astro (PR #44274) and the root now redirecting to docs (PR #44276). On the stability front, the core team landed a fix to expire stale session locations (PR #44275), addressing a class of permission-related staleness bugs. The community remains highly focused on long-standing issues around memory usage (#20695), sandboxing (#2242), and session reliability (#43277), signaling a need for more robust production hardening even as new features land.

## Releases

No new releases in the last 24 hours. The most recent stable version referenced in issues is **v1.18.21**.

## Hot Issues

1. **[#20695 — Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)** — The central tracking issue for memory leaks is still the most active thread (135 comments, 104 👍). Maintainers are asking for heap snapshots, not LLM-generated guesses. *Why it matters:* Memory issues remain the top community blocker.

2. **[#2242 — Is there a way to sandbox the agent?](https://github.com/anomalyco/opencode/issues/2242)** — 83 comments, 71 👍. Users are asking for macOS seatbelt-style or similar OS-level sandboxing to restrict agent file access. Still open after a year, indicating this is a hard problem.

3. **[#8751 — Hot-reload agents, skills, and commands](https://github.com/anomalyco/opencode/issues/8751)** — 95 👍 shows strong desire for invalidating and reloading configs while OpenCode is running. Developer workflow friction.

4. **[#4714 — TUI: Search for string in session buffer](https://github.com/anomalyco/opencode/issues/4714)** — A long-lived feature request (45 👍) for an editor-style "find" in the terminal UI.

5. **[#43277 — Sessions permanently stuck during normal use](https://github.com/anomalyco/opencode/issues/43277)** — Reports of sessions that survive reboots in a broken state are a serious reliability concern. Only 1 day old but critical.

6. **[#30662 — Auto session title generation fails for opencode provider models](https://github.com/anomalyco/opencode/issues/30662)** — A concrete root-cause analysis for a silent failure on `big-pickle` (managed gateway) models.

7. **[#44254 — Loop exits silently on orphaned interrupted tool](https://github.com/anomalyco/opencode/issues/44254)** — A new bug where mid-stream provider failures leave prompts unanswered with no error surface. Directly related to PR #44271.

8. **[#44044 — Managed gateway kills turns mid-stream](https://github.com/anomalyco/opencode/issues/44044)** — Two months of logs showing intermittent 503s and silent hangs with no client timeout on the managed `opencode` provider.

9. **[#44201 — Error: no such column: name on fresh install v1.18.21](https://github.com/anomalyco/opencode/issues/44201)** — A database schema mismatch blocking first-run users is a release-blocker class bug.

10. **[#44267 — Empty final message on auto-rejected permission in `opencode run`](https://github.com/anomalyco/opencode/issues/44267)** — The exit code is 0 with zero bytes of output, making CI failures silent and hard to debug.

## Key PR Progress

1. **[#44275 — fix(core): expire locations from session activity](https://github.com/anomalyco/opencode/pull/44275)** — Adds a `LocationActivity` service with idle deadlines and TTL management for cached locations. Core maintainer (thdxr). *Merged.*

2. **[#44274 — feat(www): rebuild site with Astro](https://github.com/anomalyco/opencode/pull/44274)** — Replaces the Blume-based site with a standard Astro build, adding Pagefind search and link validation. *Merged.*

3. **[#44277 — fix(tui): preserve rollback-compatible tab state](https://github.com/anomalyco/opencode/pull/44277)** — Keeps the retired `unread` key for backward compatibility with older beta clients. *Merged.*

4. **[#44279 — fix(core): extend FFF home protection to descendant locations](https://github.com/anomalyco/opencode/pull/44279)** — Prevents persistent indexing when a worktree contains the user home directory, a security/correctness fix.

5. **[#44271 — fix(ai): preserve raw provider error payload on responses streams](https://github.com/anomalyco/opencode/pull/44271)** — Retains structured error detail (`param`, `type`, `headers`) that was previously flattened to a message prefix. Directly addresses diagnostics gaps in #44044.

6. **[#44264 — feat(session): add suffix compaction](https://github.com/anomalyco/opencode/pull/44264)** — Experimental `compaction.mode: "suffix"` alongside the default prepend mode. A new memory-mitigation strategy.

7. **[#40125 — feat(opencode): Allow per-MCP-server trust configuration](https://github.com/anomalyco/opencode/pull/40125)** — Adds fingerprint pinning and `caFile` support for MCP servers, addressing security gaps in #40111 without globally disabling verification.

8. **[#44270 — fix(tui): avoid premature environment sync](https://github.com/anomalyco/opencode/pull/44270)** — Prevents the app-level sync from running against an optimistic session that doesn't exist on the server yet. *Merged.*

9. **[#44269 — fix(console): proxy inference without parsing](https://github.com/anomalyco/opencode/pull/44269)** — Forwards legacy `/zen` requests to `/inference` without consuming the body stream — a pure passthrough optimization.

10. **[#38393 — fix(a11y): expose streaming assistant content to screen readers](https://github.com/anomalyco/opencode/pull/38393)** — A long-delayed accessibility fix (closed after a month) making streamed content visible to assistive tech.

## Feature Request Trends

- **Hot-reload everything**: The #8751 request is part of a broader theme — users want configs (agents, skills, commands) to be mutable without restarting the TUI.
- **Session reliability & compacting**: Beyond just "fix leaks," users are asking for explicit control over session memory management (e.g., suffix compaction in #44264).
- **TUI ergonomics**: String search (#4714), tab shortcuts (#37077), and fork buttons on assistant messages (#36960) all point to users wanting a more familiar editor-like experience.
- **Security & permissions**: Beyond sandboxing (#2242), the SSRF report on `webfetch` (#36376) and per-MCP trust config (#40125) show a community that is security-conscious and wants granular control.

## Developer Pain Points

- **Provider error opacity is a recurring theme**: Multiple issues (#44044, #44254, #44267) involve silent failures where the TUI or CLI exits with no actionable error. The ecosystem is increasingly multi-provider and gateway-based, which amplifies this.
- **Memory management remains the #1 reliability blocker** (#20695): the megathread has 135 comments and a maintainer explicitly asking for snapshots over suggestions. The longer it stays open, the more it drives user frustration.
- **Session corruption and "stuck" states** (#43277): the fact that a bad state survives reboots is especially troubling for a tool that is core to daily workflows. This is likely tied to the SQLite storage layer, which also causes the fresh-install crash (#44201).
- **MCP protocol maturity**: With dozens of MCP servers, tool definitions flooding every prompt is a real token-cost problem (#35376). The community is asking for lazy-loading and per-server trust config, not just "more integrations."

*Digest generated from public GitHub data for anomalyco/opencode on 2026-08-23.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-23

## Today's Highlights
Windows support remains the dominant community concern, with multiple bugs around ConPTY rendering, terminal keybindings, and path separator issues drawing significant attention. The core team is actively addressing these: a fix for ConPTY autowrap drift (#8485) and bundled Node runtime for faster startup on Windows (#8474) landed this week. Additionally, auto-compaction continues to be a hot topic, with a high-engagement bug report (#6879, 18 👍) highlighting that context overflow protection fails before provider rejection.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#6879 — Auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)** — **18 👍, 20 comments**  
   The most-voted open bug: in a 2-hour agentic turn on gpt-5.6-sol, context climbed past the compaction threshold and only kicked in when the API rejected the request at 373k tokens. Community wants compaction checks after every agent turn, not just at threshold crossing. High urgency for long-running autonomous sessions.

2. **[#7547 — How do you use Pi on Windows?](https://github.com/earendil-works/pi/issues/7547)** — **39 comments**  
   A meta-issue probing the fragmented Windows usage landscape (WSL vs native, various terminals). The community is actively reporting pain points, making this the defacto hub for Windows-related feedback.

3. **[#7130 — Backspace deletes 2 chars in Kitty (Kitty protocol release events not filtered)](https://github.com/earendil-works/pi/issues/7130)** — **11 comments**  
   Terminal protocol interop issue: Pi's editor isn't filtering Kitty keyboard protocol release events, causing double-deletion. Related downstream issue #8442 shows similar problems in herdr panes where legacy `0x7f` bytes are ignored.

4. **[#8167 — Cannot pick a model with built-in llama.cpp support](https://github.com/earendil-works/pi/issues/8167)** — **9 comments**  
   Models from llama-server in router mode don't appear in the model list despite working via `/llama`. The community wants preset-based model discovery, addressed by PR #8479.

5. **[#8468 — Github Copilot fails with timeout](https://github.com/earendil-works/pi/issues/8468)** — **5 comments**  
   Login timeout regression when using Copilot as a provider. Users report it's blocking their workflow, though the PR #8254 fix is pending release.

6. **[#8376 — Make interactive model selection persistence configurable by scope](https://github.com/earendil-works/pi/issues/8376)** — **5 comments**  
   Users want `/model` selections to persist per-session, per-directory, or globally via a `modelSelectionScope` setting. Currently the persistence behavior is fixed, which surprises users who switch projects.

7. **[#7885 — npm search not indexing newly published pi-packages](https://github.com/earendil-works/pi/issues/7885)** — **5 comments**  
   New pi-packages fail to appear in the gallery because npm search isn't indexing them (nothing since Aug 4). Affects extension discoverability and the ecosystem's growth.

8. **[#8441 — Windows "Path outside repository" for all tools with explicit path argument](https://github.com/earendil-works/pi/issues/8441)** — **2 comments**  
   Separator mismatch in containment check on Windows: forward-slash paths from tools are rejected even when they resolve inside the repo. Likely affects every file-touching tool on Windows.

9. **[#8434 — TUI unresponsive and input echoing in v0.84.2](https://github.com/earendil-works/pi/issues/8434)** — **2 comments**  
   Regression on Ubuntu 24.04: `/login` and other slash commands echo without executing. In VS Code terminals, input shows garbled ASCII. High severity for core UX.

10. **[#8484 — Windows editor view scrolls to top / cursor lost below fold (ConPTY autowrap drift)](https://github.com/earendil-works/pi/issues/8484)** — **2 comments**  
    ConPTY commits line-wrap eagerly when the last column is written, so full-width editor borders cause relative `\r\n` navigation to advance two rows. Fixed by PR #8485 this week.

## Key PR Progress

1. **[#8474 — feat(coding-agent): bundle Node runtime](https://github.com/earendil-works/pi/pull/8474)** — *Closed*  
   Dramatically reduces file count for `pi-coding-agent`, improving startup on slow IO and Windows Defender-heavy machines. Directly addresses a top Windows pain point.

2. **[#8485 — fix(tui): disable autowrap around main-screen renders to prevent ConPTY drift](https://github.com/earendil-works/pi/pull/8485)** — *Closed*  
   Fixes #8484 by toggling autowrap off during full-width line renders on Windows/ConPTY. Targeted fix for the cursor-loss bug.

3. **[#8486 — feat(tui): add editor-scroll capture and verification tooling](https://github.com/earendil-works/pi/pull/8486)** — *Closed*  
   Companion tooling for #8485: scriptable minimal TUI app that simulates editor events (F5 setText rewrite, F6 history cycle) on the real `TuiMainScreen` + `Editor` stack, enabling regression testing.

4. **[#8479 — fix: expose unloaded llama.cpp presets](https://github.com/earendil-works/pi/pull/8479)** — *Closed*  
   Fixes #8167: llama-server presets declared via `--models-preset` are now selectable in the model picker even before loading. Improves llama-swap compatibility.

5. **[#8488 — feat(ai): add MindsHub provider](https://github.com/earendil-works/pi/pull/8488)** — *Closed*  
   Adds MindsHub as a built-in `pi-ai` provider: one API key, one endpoint, access to Claude, GPT, Gemini, Kimi, DeepSeek, Qwen, GLM. Expands multi-provider support.

6. **[#8487 — fix(coding-agent): expose finish reason compatibility override](https://github.com/earendil-works/pi/pull/8487)** — *Open*  
   Makes the finish-reason override part of the public API types (it was already in the implementation). Closes #8460.

7. **[#8482 — docs(coding-agent): point custom footer docs at ctx.getContextUsage()](https://github.com/earendil-works/pi/pull/8482)** — *Open*  
   Fixes incorrect docs referencing a nonexistent API. Small but prevents developer confusion.

8. **[#8295 — feat(coding-agent,tui): add locale switching via /settings](https://github.com/earendil-works/pi/pull/8295)** — *Closed*  
   Adds English/Simplified Chinese locale switching, `setLocale()` on SettingsManager, and runtime locale validation. Internationalization progress.

9. **[#7148 — feat(coding-agent): Experimental loadout management](https://github.com/earendil-works/pi/pull/7148)** — *Open*  
   Draft PR for `/loadout` to enable/disable extensions mid-session, persisted across session resumption. Still needs confirmation but opens extension management flexibility.

10. **[#8459 — fix(tui): keep / and - inside fullscreen double-click word selection](https://github.com/earendil-works/pi/pull/8459)** — *Closed*  
    Fixes `Intl.Segmenter` treating `/` and `-` as word boundaries, so double-clicking paths selects the whole path instead of one component. Quality-of-life UX fix.

## Feature Request Trends

1. **Provider ecosystem expansion** — Requests for MindsHub (#8489), Parasail (#8450), and new DeepSeek vision models (#8438, #8469) show the community wants more built-in providers. The gateways (one key, many models) pattern is particularly popular.

2. **Compaction intelligence** — Multiple requests (#8464, #8452, #8498) push for smarter compaction: detecting output-limit continuation, merging summaries for state fidelity, and ensuring retained tails respect token budgets even with trailing tool-result turns.

3. **TUI configuration depth** — Users want finer control: per-block default expand/collapse (#8448), model display names in selectors (#8429), scoped model selection persistence (#8376), and viewport primitives for extensions (#4861).

4. **Memory infrastructure** — The proposed SQLite-backed memory extension (#8385) with passive mirror, active notebook, and distillation layers indicates interest in persistent, queryable session memory beyond the context window.

5. **Remote/local TUI split** — Running the TUI locally while a RemoteSession handles tools/file access (#8481) suggests a multi-machine workflow is an emerging use case.

## Developer Pain Points

1. **Windows is fragile** — Six separate Windows-specific issues this week: ConPTY scrolling (#8484), path separator containment (#8441), keybinding conflicts (#8372), slow startup from Defender (#8474), TUI input regressions (#8434), and the general fragmentation question (#7547). Windows support is clearly the weakest platform experience.

2. **Compaction is not aggressive enough** — Losing a 2-hour session to context overflow (#6879) before compaction triggers is the top complaint. Users want proactive middle-of-run compaction (#8464), not reactive recovery at the provider limit.

3. **Terminal protocol interop is rough** — Kitty keyboard protocol double-deletes (#7130), herdr legacy byte ignores (#8442), and ConPTY rendering drift (#8484) show that modern terminal protocol handling remains a reliability gap.

4. **Extension discoverability broken** — npm search not indexing new pi-packages (#7885) blocks the entire extension ecosystem's growth. Authors are publishing but users can't find packages.

5. **Regression risk in TUI updates** — The v0.84.2 upgrade broke the TUI on Ubuntu (#8434) and introduced model selector display issues. The community is watching release quality closely, though the quick turn-around on fixes (#8485) is encouraging.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-23

## Today's Highlights

v0.22.0 shipped, though detailed changelog notes are pending. The review-loop ecosystem continues to dominate development activity, with major investments in convergence advisories, Aone Code integration, and execution-grade verification. A security-sensitive discussion around code execution privileges in the review pipeline has emerged, accompanied by a batch of VS Code companion enhancements and several high-priority bug fixes targeting session management and memory-related crashes.

## Releases

- **v0.22.0** — Latest stable release. Changelog details are pending at [release page](https://github.com/QwenLM/qwen-code/releases).
- **v0.21.14-nightly.20260822.7a4566cb3b** — Nightly build that backports the review-loop instability explanation feature ([#9461](https://github.com/QwenLM/qwen-code/pull/9461)), which now cites specific files with recurring findings, along with CI fallback fixes.

## Hot Issues

1. **[#9556](https://github.com/QwenLM/qwen-code/issues/9556) — Security: code execution as invoking user in review pipeline** — Open discussion on whether the review pipeline should keep granting code execution with the invoking user's privileges. Every unresolved finding across 20 review rounds on #9221 shares this precondition, making this a critical security decision requiring maintainer input. (8 comments)

2. **[#9733](https://github.com/QwenLM/qwen-code/issues/9733) — Loop detection false-positives** — Legitimate verification cycles (write→run→edit→re-run) trigger loop detection and terminate turns that can't resume without human intervention. Particularly painful for unattended multi-stage automation runs. (4 comments)

3. **[#9198](https://github.com/QwenLM/qwen-code/issues/9198) — OOM and terminal corruption** — User reports out-of-memory after running for over a week (on a 1TB server!), plus terminal corruption where copy/paste and scrolling break. Multiple sessions disabled to mitigate. Community notes Kimi Code handles the same workload fine — the memory issue is Qwen-specific. (5 comments)

4. **[#9278](https://github.com/QwenLM/qwen-code/issues/9278) — /review convergence advisory design** — Documentation issue preserving the design for publish-time convergence advisories. Describes an "out-of-control loop" where review findings generate fixes that enlarge diffs → more findings → more context. The `AGENTS.md` "after 5 rounds only Critical" prose is the only damper. (9 comments)

5. **[#9699](https://github.com/QwenLM/qwen-code/issues/9699) — Dependency CVE audit breaks all PRs** — `npm audit` reports 8 vulnerabilities (1 high) in existing dependencies, failing CI on every PR since 2026-08-21, regardless of branch or author. Blocking all merges until resolved. (4 comments)

6. **[#8102](https://github.com/QwenLM/qwen-code/issues/8102) — Deterministic tool-execution boundaries** — Long-running proposal for a trustworthy agent runtime: keep the LLM outside the trust boundary, make the runtime deterministically constrain/authorize/observe tool actions. Signed 17 comments deep with broad scope (security + core). (17 comments)

7. **[#9757](https://github.com/QwenLM/qwen-code/issues/9757) — Auto Mode classifier unavailable with OpenRouter** — Auto Mode consistently fails on OpenRouter, falling back to manual approval. Related PR #9758 aiming to fix reasoning-disable emission is already in flight. (3 comments)

8. **[#9002](https://github.com/QwenLM/qwen-code/issues/9002) — SDK rejects `permission_mode="auto"`** — Python SDK client-side validation rejects a value the CLI supports. Simple fix; closed for a while but refreshed with new activity. (6 comments)

9. **[#9695](https://github.com/QwenLM/qwen-code/issues/9695) — Deferred review findings bot** — Auto-generated list of verified findings from PR #9655 whose fixes lie outside that PR's footprint. Maintainers can convert any item into a dedicated issue or PR. (4 comments)

10. **[#9706](https://github.com/QwenLM/qwen-code/issues/9706) — Auto session title echoes prompt example** — Auto-generated session titles literally repeat `"Fix login button on mobile"` from the title-generation system prompt, even in unrelated sessions. Quality issue that looks unprofessional and confusing. (4 comments)

## Key PR Progress

1. **[#9740](https://github.com/QwenLM/qwen-code/pull/9740) — Execution-grade review verification** — New `qwen review ab-drive` subcommand runs one script against both the PR worktree and `base-tree` to produce paired captures with byte-identical comparison. Structural upgrade for review evidence quality.

2. **[#9748](https://github.com/QwenLM/qwen-code/pull/9748) — Worktree cleanup permission repair** — End-of-job sweep now repairs write permissions before giving up on removing leftover review worktrees, reducing orphaned trees and disk leaks across CI runs.

3. **[#9729](https://github.com/QwenLM/qwen-code/pull/9729) — Session↔PR binding backfill** — Extends the session↔PR binding feature with an on-demand daemon route that scans persisted sessions and backfills PR bindings for sessions predating the feature, plus merge-state refresh.

4. **[#9758](https://github.com/QwenLM/qwen-code/pull/9758) — OpenRouter reasoning-disable fix** — Emits OpenRouter's native reasoning disable when `includeThoughts: false`, fixing Auto Mode classification issues with OpenRouter endpoints — pairs with #9757.

5. **[#9691](https://github.com/QwenLM/qwen-code/pull/9691) — Autofix budget increase** — Raises repair agent budget from 18 to 45 minutes, with corresponding bound adjustments (repair cap 20m→55m, job cap 300m→330m, stale threshold 330→360). A practical response to loop-timeout failures.

6. **[#9626](https://github.com/QwenLM/qwen-code/pull/9626) — Persisted session lifecycle repair** — Makes delete/archive/unarchive work even with empty, torn, or legacy orphaned transcripts; classification moves to exact regular files — significant reliability improvement for long-lived sessions.

7. **[#9659](https://github.com/QwenLM/qwen-code/pull/9659) — Content-anchored incremental review rounds** — Relanded on main after 20 reviews and 166 inline comments on the prior stacked PR. Anchors review findings to content rather than line numbers to survive rebases; follow-up (per-file verdicts) opens once this lands.

8. **[#9737](https://github.com/QwenLM/qwen-code/pull/9737) — Enforce utils leaf-layer dependency direction** — Makes `packages/cli/src/utils/` a true leaf by mechanically preventing imports back into config, ui, i18n, serve, and commands. Architectural hygiene for the CLI package (#9146 slice).

9. **[#9394](https://github.com/QwenLM/qwen-code/pull/9394) — DingTalk Workspace channel** — Built-in channel via DWS CLI profiles. Supports DMs, @mentions, ambient groups, document-mention notifications, native todos, source-scoped sessions. Still needs human review; label `autofix/needs-human`.

10. **[#9582](https://github.com/QwenLM/qwen-code/pull/9582) — Telemetry replay rollback** — Makes usage telemetry replays undoable when session swaps fail, preventing double-counted usage data and inaccurate user-facing metrics.

## Feature Request Trends

- **Review-loop convergence tooling** dominates: content-anchored findings, convergence advisories that cite offending files, execution-grade verification, and instruments to diagnose "why isn't this settling" — all actively receiving PRs and issues.
- **Aone Code (Alibaba's internal review platform) support** is being systematically completed: metadata fetching, comment-status threading, presubmit, inline anchoring for removed lines.
- **VS Code companion enhancements**: WebShell transcript behind experimental flag, drag-drop file support, CSP widening for artifacts — a burst of IDE integration work.
- **Daemon/session improvements**: per-session model restoration, unanswered HITL re-hang after load/resume, cross-session messaging behind a gate.
- **Trustworthy agent runtime**: deterministic tool-execution boundaries still generating active discussion toward a more trustworthy agent runtime.

## Developer Pain Points

1. **OOM and memory leaks in long-running sessions** — A server with 1TB RAM OOMs run to exhaustion; Web Shell transcript retention is hacked to bound memory; session history produces placeholder messages when tools complete normally but history was missing.
2. **Loop detection false positives** — Legitimate verification cycles kill unattended turns that can't resume without human interaction. Loop detection needs to distinguish state-advancing sequences from actual loops.
3. **CI blocking due to dependency CVEs** — A single vulnerable dependency in existing code blocks all PRs, indicating the need for a softer CI posture on pre-existing audit findings.
4. **Review loop instability** — Convergence advisories and instability explanations exist but the loop still doesn't settle in practice; rounds often produce 20+ review passes with 100+ inline comments.
5. **Session model restoration inconsistency** — Resumed daemon sessions use process-wide defaults rather than the model that session last used, causing surprise model switches.
6. **Terminal display issues** — Auto session titles echoing prompt examples verbatim; CP issues in terminal rendering; Web Shell pinning latency — small but visibly annoying UX bugs.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-23

## Today's Highlights

The CodeWhale TUI ecosystem is mid-cycle on a major architectural chapter: EPIC-005's crate decomposition continues to reshape the codebase, with FEAT-018 moving the TUI utility command group onto the new command-shape system (#5525). Concurrently, release v0.9.11 is being prepared on a clean non-benchmark branch (#5542), while a substantial supervised-operation stack PR introduces lifecycle outboxes and per-session control sockets (#5535). Pricing logic also gets a region-aware correction for DeepSeek V4 weekend off-peak billing in Beijing (#5545).

---

## Releases

No new releases were published in the last 24 hours. The community is watching PR #5542 (v0.9.11 release candidate), which explicitly excludes the `benchmarks/pi-agent-parity/**` tree and its release-lane ancestry to keep the release branch clean.

---

## Hot Issues

**1. EPIC-005: CodeWhale TUI Crate Decomposition (Umbrella)** — [#5316](https://github.com/Hmbown/CodeWhale/issues/5316)
The master tracking issue for the crate decomposition effort. With 12 comments and sustained activity since August 10, this is the structural backbone of current development. All sub-EPICs and FEATs report here, making it the best single entry point for understanding the architecture migration.

**2. Persist child tool approvals through the durable receipt path** — [#5543](https://github.com/Hmbown/CodeWhale/issues/5543)
A subtle correctness bug: child agents waiting for parent decisions don't use the durable approval receipt path. The parent writes an `Asked` receipt before `ApprovalRequired`, but the child's path diverges. This matters because it breaks auditability and crash-recovery guarantees for multi-agent tool approvals.

---

## Key PR Progress

**1. fix(pricing): bill whole Beijing weekends off-peak for DeepSeek V4** — [#5545](https://github.com/Hmbown/CodeWhale/pull/5545)
Corrects `deepseek_is_peak` to use Beijing time for weekend detection. DeepSeek's new policy (effective August 23, 2026) makes weekends off-peak all day. The prior UTC-hour-only logic could mis-bill by up to 8 hours on the weekend boundary. **This is a high-impact financial fix for any user running weekend batch workloads in Asia.**

**2. feat(tui): add multi-file read_lints operation** — [#5524](https://github.com/Hmbown/CodeWhale/pull/5524)
Extends the model-visible `lsp` tool with `read_lints` for multiple existing workspace-relative files, reusing the session `LspManager` transport pool instead of spawning new language-server lifecycles. This addresses scope from #4070 and should reduce LSP startup latency when linting many files.

**3. feat(web): move docs/subagents and docs/mcp onto the dictionary spine** — [#5544](https://github.com/Hmbown/CodeWhale/pull/5544)
Next group in the #5337 documentation-i18n series after #5520. Eliminates 34 `isZh` conditional branches across `docs/subagents` and `docs/mcp`, wiring both into `check-locales.mjs`'s `OPTIONAL_FILES`. This steadily erodes the bilingual-docs maintenance burden.

**4. refactor(tui): adopt command shapes in utility group (FEAT-018)** — [#5525](https://github.com/Hmbown/CodeWhale/pull/5525)
Converts all seven TUI utility command files (including `/a…`) to the external command shapes from FEAT-014/FEAT-015. Commands stay in `codewhale-tui` but get a new execution boundary — a key step in EPIC-005's decomposition.

**5. release: prepare Codewhale v0.9.11** — [#5542](https://github.com/Hmbown/CodeWhale/pull/5542)
Non-benchmark release candidate built on clean `main`. PR head `accfa93e` is byte-identical to the fully gated local build. Intentionally excludes `benchmarks/pi-agent-parity/**` to keep release-lane ancestry separate. Signals a soon-to-land stable release.

**6. chore(deps): bump portable-pty to 0.9.0** — [#1701](https://github.com/Hmbown/CodeWhale/pull/1701)
**CLOSED** after three months. Adds loongarch64 support upstream (requested in #1531) and drops the transitive duplicate `nix 0.25.1` in favor of the workspace's `nix 0.28.0`. A long-awaited dependency cleanup finally merged.

**7. Supervised operation stack: lifecycle outbox, /relaunch, per-session control socket, and goal-continuation quiet-period fix** — [#5535](https://github.com/Hmbown/CodeWhale/pull/5535)
A five-part change set on machine-readable supervision: opt-in JSONL/webhook lifecycle outbox (`turn_start`, `turn_end`, `subagent_spawn`, `sessi…`), `/relaunch` command, per-session control sockets, and a quiet-period fix for goal continuation. This is a significant step toward scriptable, externally-observable long-running sessions.

---

## Feature Request Trends

Trends are distilled from the limited 24-hour window (2 issues, 7 PRs); longer-term signals (e.g., #4070's approved scope driving #5524, #5337's docs-i18n series) point to these directions:

- **Durable, auditable multi-agent approvals** — #5543's durable-receipt gap highlights a systemic push toward crash-safe, replayable parent/child tool-approval flows.
- **Machine-readable session supervision** — #5535's lifecycle outbox and control sockets align with a broader need for programmable, externally-observable TUI sessions (JSONL/webhook hooks).
- **TUI crate architecture modernization** — EPIC-005's decomposition (FEAT-014/015/018) is in full swing; expect more command-group migrations and boundary changes in the coming weeks.
- **Regional- and timezone-aware pricing** — #5545 is a direct response to DeepSeek's new Beijing-time weekend billing policy; the pattern suggests more region-aware logic will follow.

---

## Developer Pain Points

- **UTC-vs-local timezone billing bugs**: `deepseek_is_peak` relying on UTC hours mis-priced Beijing weekends — a classic timezone-handling pitfall with direct revenue impact. Expect more TZ-aware audits.
- **Dead-lock / crash-recovery inconsistencies**: #5543's invisible child-tool approval path breaks the durable receipt guarantee, undermining auditability for multi-agent runs.
- **Language-server lifecycle churn**: The LSP tool spawning per-operation is expensive; #5524's reuse of the existing transport pool addresses a real latency complaint.
- **Release-lane contamination**: Keeping benchmark (`pi-agent-parity`) and non-benchmark release branches separate (#5542) reflects ongoing friction in release hygiene.
- **Dependency-update lag**: portable-pty 0.9.0 took three months to merge (#1701) — arch support (loongarch64) and `nix` dedup are nice, but the delay pattern suggests review-bottleneck frustration persists.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*