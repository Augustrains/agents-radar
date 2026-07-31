# AI CLI Tools Community Digest 2026-07-31

> Generated: 2026-07-31 01:26 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report — 2026-07-31

## 1. Ecosystem Overview

The AI CLI tooling landscape is in a stabilization phase, with all major players shipping few or no releases this week while prioritizing reliability, bug-fixing, and architectural refactoring. **Agent orchestration reliability** is the dominant cross-cutting concern, appearing in near-identical forms across Claude Code, Gemini CLI, Copilot CLI, and Qwen Code — specifically around subagent failures being misreported as successes, runaway token consumption, and session resumability gaps. Windows stability remains the single largest platform gap, with OpenCode, Codex, Qwen Code, and Kimi all reporting Windows-specific crashes, rendering bugs, and packaging failures. Cost transparency and rate-limit economics are emerging as a second-order systemic issue, with users across Copilot CLI, OpenCode, and Claude Code reporting billing surprises, silent credit drains, and inadequate usage visibility. Projects are converging on common architectural responses: telemetry, observability, guardrails, and single-binary distribution.

## 2. Activity Comparison

| Tool | Issues (24h) | PRs (24h) | Release Status |
|------|-------------|-----------|----------------|
| **Claude Code** | ~10 hot issues; 1 new config regression (#82761) | No meaningful PR activity; 1 closed/irrelevant | No new release |
| **OpenAI Codex** | 50 issues; 10 hot (top: #31573 OAuth at 66👍) | 48 PRs; 10 merged (robustness/internal infastructure) | No new release; latest v0.146.0-alpha.3.1 |
| **Gemini CLI** | 10 hot issues; 2 P1s pending retest | 10 significant merged PRs (perf, security, env ordering) | v0.55.0-nightly (changelog-only) |
| **GitHub Copilot CLI** | ~10 hot issues; 3 closed | No PRs updated | v1.0.77 (OAuth web flow, sandbox bypass) |
| **Kimi Code** | 3 hot issues (1 critical 429 outage) | 1 PR merged (Python GC fix in hooks) | No new release |
| **OpenCode** | 10 hot issues (top: #39653 Sol overload) | 10 merged PRs (TUI improvements, crash fixes) | v1.18.10 (Modal discovery, UI polish) |
| **Pi** | 10 hot issues (stuck-promise cascade; 4 issues trace to root cause) | 10 PRs (protocol work, Wayland fix, grapheme widths) | No new release |
| **Qwen Code** | 9 hot issues (5 converter bugs in week) | 10 merged PRs (converter fixes, worktree isolation) | v0.21.1-nightly (CI fixes only) |
| **DeepSeek TUI / CodeWhale** | 10 hot issues (refactor epics dominate) | 10 PRs (refactor layers, release close-out, keyboard fixes) | v0.9.2 (final legacy name; rebranded) |

## 3. Shared Feature Directions

| Direction | Tools | Specific Needs |
|-----------|-------|----------------|
| **Subagent/Agent reliability & observability** | Claude Code, Gemini CLI, Copilot CLI, Qwen Code | Stop-runaway-tokens (#82104), no false "GOAL success" (#22323), no silent empty returns (#4293), configurable turn limits (#8168), agent status surfaced beyond TUI (#4022) |
| **Cost/credit visibility & caps** | Claude Code, Copilot CLI, OpenCode, Kimi | Live token usage, pre-limit warnings (#4295), no post-kill billing (#82104), 2× Plus quota (#36213), "server overloaded" provider status (#39653) |
| **Windows parity & stability** | Codex, OpenCode, Qwen Code, Kimi | Crashes (CrBrowserMain #32683, heap corruption #72377), sandbox failures, installer SHA-256 mismatches, 16-bit exec errors (#37628), freeze-with-spinner (#2570) |
| **Session lifecycle & resumability** | Claude Code, Copilot CLI, OpenCode, Pi | Unresumable background transcripts across identity boundary (#77730), reopen closed side chats (#27716), cross-device continuity (#34804), no stale-session crash (#39704) |
| **Local/self-hosted & 3rd-party provider support** | Gemini CLI, OpenCode, Pi, Qwen Code | MCP flattening for non-OpenAI providers (#26234), Ollama/OpenRouter/Bedrock first-class support, LiteLLM proxy built-in (#29935), OpenCode LAN discovery |
| **Configuration transparency & guardrails** | Qwen Code, OpenCode, DeepSeek/CodeWhale | Deterministic redaction before sending (#26525), host tool-invocation guard (#8032), enforce read-only plan mode (#39491), worktree-scoped settings (#8138) |
| **Persistent memory & context management** | Kimi Code, Gemini CLI, Qwen Code | Dual-mode memory (auto+manual) (#1283), auto-compression on overflow (#28488), no low-signal memory endless retries (#26522), workspace-qualified memory (#8056) |
| **Single-binary/distribution simplification** | DeepSeek/CodeWhale, Gemini CLI, Qwen Code | 14.878-line monolith split (#3306), one executable, library-backed TUI; Node 20 EOL rise to Node 22/24 (#28603) |

## 4. Differentiation Analysis

**Claude Code** is the most orchestration-heavy, with the deepest agent-hierarchy and hooks model. Its community surfaces issues at a granular protocol level (TaskStop doesn't stop children, scheduled one-shots fail silently) — but has the least PR activity this week, indicating maintainer bottleneck. It has the most sophisticated skill/frontmatter ecosystem and multi-agent orchestration ambitions; its pain points are scaling costs and configuration regressions, not feature gaps.

**OpenAI Codex** distinguishes itself by shipping visibly through merged PRs — 48 PRs, 10 merged — targeting server/app internals (streaming buffers, sandbox event normalization, protocol exports). It's investing heavily in enterprise automation support (`enterprise_cbp_automation`) and remote filesystem robustness. Its pain: Windows desktop and "Model metadata plumbing" bugs (gpt-5.6-luna MultiAgent V1/V2 mismatch) — a tool where architecture moves fast but platform parity lags.

**Gemini CLI** is the most P1-bug-driven project — two critical P1s pending retest (#22323 false-success, #21409 indefinite hang). Its maintainers respond quickly with targeted fixes (diff hunk glob explosion, MCP OAuth refresh) but the community is pessimistic enough to suggest "don't use subagents at all" as a workaround. Signal: reliability-first is the differentiator.

**GitHub Copilot CLI** is distinguished by its tight GitHub enterprise integration and AI-credit transparency debates. The community is focused on credit counting and silent background consumption, plus web-flow OAuth as a corporate-friendly default. It has the fewest PRs this week — likely a mature, lower-velocity product.

**Kimi Code** is the least active and most feature-starved community — its top ask remains "memory system" and it has a single critical outage (#2571) and a mysterious Windows freeze (#2570). The project is early-stage, and its roadmap is thinner than others.

**OpenCode** is the most community-driven and contributor-friendly — one contributor (kitlangton) runs a streak of TUI features. It's iterating fastest on UI/UX (tabbed interface, hot-reload, open menu, session inheritance) while simultaneously having notable plan-mode-security and web-UI maturity gaps. It's the "community kernel" of the group.

**Pi** is the most protocol-focused — building a transport-neutral wire protocol and runtime-neutral client, adding OpenAI `background: true` support, and exploring loadout management. Its most painful reliability issue is a stuck-promise cascade that wedges model runtime and blocks `/login` and `/scoped-models`. It's a project aiming at headless/remote sessions and provider parity.

**Qwen Code** is in an aggressive stabilization push — nightly releases, CI fixes, and converter bug fixes (5 Anthropic converter bugs this week) — plus architectural work (Goal v3 adoption, OpenAI Responses API generator). It's focused on trustworthy agent runtime with a host tool-invocation guard. The community is heavily Chinese-language and has a strong "local model" preference.

**DeepSeek TUI / CodeWhale** is rebranded and in the middle of a massive refactor (18 packages, 771k lines, 87% in one crate). Its community and its maintainers are co-developing the refactor via mergeable layers, with active Gherkin acceptance tests. It's the most "single-binary and library-backed TUI" focused of the group, and closest to a "real product" naming/branding transition.

## 5. Community Momentum & Maturity

**Highest momentum:** **OpenCode** (contributor throughput, feature velocity, TUI experience) and **OpenAI Codex** (48 PRs, robust issue ecosystem, strong engagement metrics). **Qwen Code** has high momentum with a nightly cadence and auto-fixed E2E fleet.

**Highest community engagement per issue:** **Claude Code** (#36151 at 530👍, #82104 at high-urgency billing) and **Codex** (#31573 at 66👍, #13200 at 58👍) show the strongest "demand signal" community, with high upvotes and long threads. **Pi** and **DeepSeek/CodeWhale** have smaller but highly technical, design-literate communities (protocol PRs reviewed in-depth, refactor epics co-developed).

**Most at-risk of trust erosion:** **Gemini CLI** (false-success subagent reports, indefinite hangs that force disabling subagents entirely) and **Copilot CLI** (silent credit drains, subagent empty returns with no logging). **Kimi Code** has the most fragile community confidence — a single 429 outage blocking core functionality for paid users.

**Most mature lifecycle:** **DeepSeek/CodeWhale** and **Claude Code** are in "rebuild and refactor" phases rather than new features, which often signals product maturity and an existing power-user base. **Codex** and **OpenCode** are in "feature expansion" with new architecture investment. **Kimi** and **Gemini** are in "reliability survival" mode.

## 6. Trend Signals

### 1. Agent orchestration trust is the #1 barrier to enterprise adoption.
False-success reporting ("GOAL" termination when hitting MAX_TURNS), silent empty subagent returns, and kill-switch failures are not just bugs — they are **safety and audit failures** that prevent automation from moving beyond demos. Enterprises will demand: deterministic termination, subagent transaction IDs, and per-turn cost/usage logging as first-class features.

### 2. Cost telemetry is the next "killer feature."
Across 5 tools (#4295, #4308, #82104, #37748, #2571), users are asking for **forensic token/credit accounting**, not just estimates. Expect "usage as a first-class data product" — per-session, per-tool-call, per-subagent billing waterfalls — to be a differentiator in the next release cycle.

### 3. Windows is the new "Linux-on-desktop."
Windows-specific crashes and packaging failures are surfacing at a rate that will push vendors to either (a) fund Windows-first CI/test infrastructure or (b) lose the enterprise market. The pattern mirrors 2010s Linux desktop fragmentation — except this time the tool is the product, not the OS.

### 4. Local/self-hosted providers are becoming first-class citizens.
Ollama, LMStudio, OpenRouter, AWS Bedrock, LiteLLM — the demand is no longer "can I use a local model?" but "is my CLI provider-agnostic enough to treat local and cloud models identically?" Tools that assume OpenAI API compatibility as a universal substrate are losing points; those that abstract MCP namespaces and handle per-provider metadata quirks will win the self-hosted developer.

### 5. Security boundaries are shifting from sandbox to **trust boundary**.
Qwen Code's "keep model outside trust boundary" (#8102), OpenCode's plan-mode write escapability (#39491), and Qwen Code's host tool-invocation guard (#8032) all point to a trend: the **runtime is the trust anchor**, not the model. Expect "deterministic, configurable tool authorization + auditing" to be a design pattern across all CLI tools within 2 quarters.

### 6. "Stuck-promise" and silent no-op bugs are the new class of P0s.
Across Pi (#7301), Claude Code (#82761 config no-op), and Copilot CLI (#4293), the pattern is: **a silent failure that fails to fail loudly**. These are the most damaging because they are invisible until cost or time is already wasted. Expect "loud failure receipts" to become a design principle in the next generation of agent runtimes.

### 7. The refactor race is on.
DeepSeek/CodeWhale (split monolith), Gemini CLI (fixing EOL dependencies), Codex (protocol exports precomputation), and Qwen (Goal v3) are all rewriting internal architecture in parallel — while Copilot CLI and Claude Code show low PR velocity. The winners will ship the next generation of features first; the laggards will increasingly be compared unfavorably on reliability.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-31 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### 🥇 #1 — skill-creator: run_eval.py trigger detection fix
**PR [#1298](https://github.com/anthropics/skills/pull/1298)** | Author: MartinCajiao | Open | Created: 2026-06-10
- **Functionality**: Fixes the critical `run_eval.py` bug where the skill-description optimization loop reports `recall=0%` for every skill, rendering the entire optimization process useless. The fix installs the eval artifact as a real skill, fixes Windows stream reading, trigger detection, and parallel worker coordination.
- **Discussion highlights**: The most active PR in the repository, addressing the single largest blocker to skill-quality tooling. This fix unblocks the `run_loop.py` and `improve_description.py` pipelines.

### 🥈 #2 — run_eval.py Windows pipe crash fix
**PR [#1099](https://github.com/anthropics/skills/pull/1099)** | Author: joshuawowk | Open | Created: 2026-05-07
- **Functionality**: Fixes `run_eval.py` crashing on Windows when reading from subprocess pipes, manifesting as `[WinError 10038]`. Every query on Windows is recorded as "not triggered," making the tool unusable on that platform.
- **Discussion highlights**: Part of a cluster (with #1050, #1061) of Windows compatibility fixes — a major community pain point.

### 🥉 #3 — Fix Windows subprocess + encoding bugs
**PR [#1050](https://github.com/anthropics/skills/pull/1050)** | Author: gstreet-ops | Open | Created: 2026-04-27
- **Functionality**: Two 1-line Windows fixes: `subprocess.Popen(["claude", ...])` fails with `[WinError 2]` because Windows ships `claude.cmd` (PATHEXT not honored), plus cp1252 encoding handling.
- **Discussion highlights**: Complements #1099 and #1298; the community is clearly investing heavily in cross-platform reliability for skill tooling.

### #4 — document-typography skill
**PR [#514](https://github.com/anthropics/skills/pull/514)** | Author: PGTBoos | Open | Created: 2026-03-04
- **Functionality**: Typographic quality control for AI-generated documents — prevents orphan word wrap (1-6 words spilling to next line), widow paragraphs, and numbering misalignment.
- **Discussion highlights**: Addresses a universal pain point in document generation. The community finds this valuable because these issues affect nearly every document Claude generates.

### #5 — ODT skill (OpenDocument creation)
**PR [#486](https://github.com/anthropics/skills/pull/486)** | Author: GitHubNewbie0 | Open | Created: 2026-03-01
- **Functionality**: Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods) — including ODT-to-HTML conversion and template filling.
- **Discussion highlights**: Expands the ecosystem beyond PDF/DOCX, which is particularly valuable for LibreOffice and open-source ecosystem users.

### #6 — skill-quality-analyzer + skill-security-analyzer (meta skills)
**PR [#83](https://github.com/anthropics/skills/pull/83)** | Author: eovidiu | Open | Created: 2025-11-06
- **Functionality**: Two meta-skills: quality analysis across 5 dimensions (structure, documentation, examples, resources, etc.) and security analysis for skills.
- **Discussion highlights**: With the security concern in Issue #492, security analysis for skills is a timely and highly relevant addition.

### #7 — testing-patterns skill
**PR [#723](https://github.com/anthropics/skills/pull/723)** | Author: 4444J99 | Open | Created: 2026-03-22
- **Functionality**: Comprehensive testing stack coverage — Testing Trophy model, AAA pattern, React component testing, what to test vs. what NOT to test.
- **Discussion highlights**: Represents a major demand for guided testing directly in Claude Code workflows.

### #8 — self-audit skill (mechanical verification + reasoning audit)
**PR [#1367](https://github.com/anthropics/skills/pull/1367)** | Author: YuhaoLin2005 | Open | Created: 2026-06-28
- **Functionality**: Audits AI output before delivery — mechanical file verification (every claimed file exists) followed by a four-dimension reasoning audit in damage-severity order. Universal — works with any project/stack/model.
- **Discussion highlights**: Fresh PR showing continued demand for output-quality gates; pairs with the related pipeline proposal in Issue #1385.

---

## 2. Community Demand Trends

**Highest-signal demand: skill quality and reliability tooling (meta-skills).** Six of the top 10 PRs and four of the top issues revolve around fixing, evaluating, or improving the skill-creation toolchain itself. The community's most active conversation isn't about new skills — it's about making the skill-maker reliable.

Other clear trends:

| Trend | Evidence | Signal |
|-------|----------|--------|
| **`run_eval.py` and `skill-creator` are broken** | Issues #556, #1169, #1061; PRs #1298, #1099, #1050, #1323, #1261 | **Dominant** — 10+ independent reproductions of the recall=0% bug |
| **Windows compatibility** | PRs #1099, #1050; Issue #1061 | High — multiple champions submitting overlapping fixes |
| **Security of community skills** | Issue #492 (43 comments, highest) | High — trust boundary abuse under `anthropic/` namespace |
| **Org-wide skill sharing** | Issue #228 (16 comments, 8👍) | Medium — enterprise deployment friction |
| **Document-format expansion** | PRs #486 (ODT), #538/#541 (fixes) | Medium — ODF formats beyond PDF/DOCX |
| **Output-quality gatekeeping** | PRs #1367 (self-audit), #1479 (plan-file-hygiene); Issues #1385, #412 | Medium — verifying AI output before delivery |

---

## 3. High-Potential Pending Skills (Likely to Land Soon)

| PR | Skill | Why it's high-potential |
|----|-------|------------------------|
| [#1302](https://github.com/anthropics/skills/pull/1302) | **color-expert** (meodai) | Self-contained color expertise — naming systems (ISCC-NBS, Munsell, RAL), color-space selection tables, and "what to use when" guidance. Very well-scoped, definitive reference skill. |
| [#525](https://github.com/anthropics/skills/pull/525) | **pyxel** (kitao) | Retro game development via pyxel-mcp. Author is the pyxel-mcp maintainer — strong domain authority; workflow is clearly specified (write → run_and_capture → inspect → iterate). |
| [#1367](https://github.com/anthropics/skills/pull/1367) | **self-audit** (YuhaoLin2005) | Active author with a parallel pipeline proposal in Issue #1385. Universal applicability; addresses the quality-gate gap. |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** (4444J99) | Covers a major developer workflow (testing) with broad stack coverage. High practical value for daily Claude Code use. |
| [#1479](https://github.com/anthropics/skills/pull/1479) | **plan-file-hygiene** (Palo-Alto-AI-Research-Lab) | Addresses Issue #1417 — planning artifacts accumulate with no lifecycle. Early but with explicit community credit and good framing. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable skill-development tooling itself** — fixing `run_eval.py`, Windows compatibility, and trigger detection — before any individual new skill, indicating the ecosystem is maturing from "collecting skills" to "engineering skills at scale" with quality assurance, security, and cross-platform reliability as the critical path.

---

# Claude Code Community Digest — 2026-07-31

## Today's Highlights

The community is heavily focused on **agent orchestration reliability** this week, with critical reports on subagent runaway token consumption after `TaskStop` (750k tokens billed post-kill) and background agent transcripts becoming unresumable across session-identity boundaries. A notable **regression in scheduled tasks** — 6 of 6 one-shots failing with 3 never dispatched and 3 killed mid-tool-call — is drawing attention from automation-dependent developers. Additionally, a new issue reports that `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` silently stopped working after v2.1.220, signaling a potential configuration regression that needs immediate investigation.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#36151 — Multi-account switching in Claude Mobile app without shared email](https://github.com/anthropics/claude-code/issues/36151)** — *148 comments, 530 👍* — The most-active issue this week. Long-running request (since March) for account separation in the mobile app. The high engagement suggests this is a top pain point for teams sharing devices or managing personal/professional identities.

2. **[#82104 — TaskStop does not stop subagent children: 750k tokens billed after kill](https://github.com/anthropics/claude-code/issues/82104)** — *2 comments* — Critical billing/reliability bug. Three defects compound: `TaskStop` on a parent doesn't stop children, users have no live usage visibility, and no cap exists. For teams on metered plans, this is potentially a very expensive failure.

3. **[#82728 — Scheduled one-shots: 6 of 6 failed](https://github.com/anthropics/claude-code/issues/82728)** — *3 comments* — Three sessions never dispatched and remained armed; three were killed mid-tool-call but recorded as successful. This affects automation reliability and could silently corrupt workflows.

4. **[#6305 — Post/PreToolUse Hooks Not Executing in Claude Code](https://github.com/anthropics/claude-code/issues/6305)** — *38 comments* — Long-running bug (since Aug 2025) on macOS. Hooks are critical for security guardrails and custom automation; the duration of this issue suggests a persistent gap.

5. **[#63566 — `/claude-api` bundled skill saturates context unconditionally](https://github.com/anthropics/claude-code/issues/63566)** — *6 comments, 7 👍* — A neutral question spikes context usage by ~77%. This impacts both cost and context-window availability, especially on Windows where the skill is bundled.

6. **[#77730 — Background agent transcripts become unresumable across session-identity boundary](https://github.com/anthropics/claude-code/issues/77730)** — *7 comments* — Forced full-context respawns (token burn) when background agent transcripts on disk can't be resumed. Affects long-running agent workflows and productivity.

7. **[#59854 — Cowork GitHub connector unusable: OAuth DCR unsupported](https://github.com/anthropics/claude-code/issues/59854)** — *5 comments, 12 👍* — The GitHub connector in Cowork fails at the OAuth level, with misleading UI state and a dead Disconnect button. High 👍 count suggests wide impact for GitHub-centric teams.

8. **[#72377 — Cowork regression: KERNEL_MODE_HEAP_CORRUPTION (0x13A) in storvsp!VspVsmbFileCreate](https://github.com/anthropics/claude-code/issues/72377)** — *1 comment, high-priority* — Windows-specific kernel crash likely due to storage virtualization; a serious stability issue for Cowork users on Windows.

9. **[#82761 — CLAUDE_AUTOCOMPACT_PCT_OVERRIDE silently stopped taking effect](https://github.com/anthropics/claude-code/issues/82761)** — *New* — Silent config no-op since v2.1.220. Developers relying on compaction control to manage context and costs will be especially affected.

10. **[#78834 — Bundled ugrep allocates 4-17 GB to search a 64 KB file](https://github.com/anthropics/claude-code/issues/78834)** — *3 comments* — Memory explosion with trailing `.{N}` bounds in regex patterns. Could crash sessions on memory-constrained Linux/WSL2 environments.

## Key PR Progress

No meaningful PR activity in the last 24 hours — the only PR (#82555) is a closed/irrelevant entry. The community is waiting on the maintainers to address the significant backlist of issues.

## Feature Request Trends

- **Multi-account / identity separation** (#36151) — Strong demand for distinct accounts across mobile and desktop without email-sharing hacks.
- **Agent model management** (#78217) — A managed default for sub-agent model selection for better cost/quality control.
- **Agent frontmatter enhancements** (#69391) — A `blocking` field for agents, mirroring the blocking behavior in skills, for deterministic orchestration.
- **Sensitive data protection** (#82734) — In-memory storage for background task outputs to avoid disk leakage; increasingly driven by security-conscious teams.

## Developer Pain Points

1. **Runaway subagent costs** — No effective stop mechanism, no usage visibility, no caps (#82104). This is the highest-urgency pain point for cost-sensitive teams.
2. **Silent configuration regressions** — `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` became a no-op after v2.1.220 with no warning (#82761); `--agents` accepts invalid JSON with exit 0 (#79527). Developers are burning tokens and debugging configs that "used to work."
3. **Session/transcript resumability** — Background work is being interrupted or lost across session boundaries (#77730), forcing expensive full-context respawns.
4. **Scheduled task reliability** — Failures that either never dispatch or misreport success (#82728) undermine trust in automation.
5. **Hook and custom-agent execution gaps** — Hooks not firing (#6305) and context saturation from bundled skills (#63566) continue to destabilize custom workflows.

---

*Digest generated from [anthropics/claude-code](https://github.com/anthropics/claude-code) issues, PRs, and releases for the 24h period ending 2026-07-31.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest
**2026-07-31**

---

## 1. Today's Highlights

No new releases shipped in the last 24 hours, but the repository saw significant activity across **50 issues** and **48 pull requests**. Windows desktop stability remains the top community pain point, with crashes, sandbox failures, and OneDrive-related disconnects dominating the issue tracker. On the development side, a wave of merged PRs focused on internal robustness—including streaming buffer efficiency, sandbox event normalization, and connector runtime improvements—signals ongoing investment in the app-server and MCP infrastructure.

---

## 2. Releases

No new releases in the last 24 hours. The most recent version referenced across issues is **codex-cli 0.146.0-alpha.3.1** (Codex App 26.721.4979.0).

---

## 3. Hot Issues

### 1. OAuth authentication fails at issuer validation
**#31573** — 31 comments, 66 👍 — [Link](https://github.com/openai/codex/issues/31573)

Free-tier CLI users cannot complete OAuth login due to issuer validation failures on Codex CLI 0.143.0. High engagement suggests a widespread auth regression affecting onboarding.

### 2. [Windows] Codex App crashes in CrBrowserMain when Browser Use opens a page
**#32683** — 29 comments, 8 👍 — [Link](https://github.com/openai/codex/issues/32683)

Pro users on Windows 10/11 hit a hard crash (`0xC0000005` in `chrome.dll`) whenever the Browser Use feature opens a page. The in-app browser is effectively unusable on Windows.

### 3. Flatten MCP namespace tools for non-OpenAI Responses API providers
**#26234** — 27 comments, 40 👍 — [Link](https://github.com/openai/codex/issues/26234)

MCP tools are serialized as `{"type": "namespace", ...}` which non-OpenAI providers (Ollama, LM Studio, OpenRouter, AWS Bedrock) cannot parse, making MCP servers useless with those backends. A long-running request (since June) with sustained community interest.

### 4. Windows Codex Desktop spellcheck detects misspellings but shows "No Guesses Found"
**#26478** — 18 comments, 25 👍 — [Link](https://github.com/openai/codex/issues/26478)

The spellcheck UI detects errors but never offers suggestions, despite native Windows spellcheck working in other apps. Cosmetic but high-visibility friction for Windows desktop users.

### 5. Work/Codex stream repeatedly disconnects on OneDrive-backed workspaces
**#35420** — 16 comments — [Link](https://github.com/openai/codex/issues/35420)

When the selected workspace is OneDrive-backed and OneDrive is degraded, Codex repeatedly fails with `stream disconnected before completion`. A niche but painful integration issue for enterprise Windows users.

### 6. `codex mcp login` fails for Slack official MCP with "Dynamic client registration not supported"
**#13200** — 10 comments, 58 👍 — [Link](https://github.com/openai/codex/issues/13200)

Enterprise users (ChatGPT Enterprise) cannot connect to Slack's official MCP server because Codex's client doesn't support dynamic client registration. High 👍 count signals strong demand for first-party MCP integrations.

### 7. VS Code extension: full Review diff page crashes while inline diff works
**#35362** — 10 comments, 13 👍 — [Link](https://github.com/openai/codex/issues/35362)

On Windows, opening the full Codex Review diff view crashes, while inline diffs render fine. Likely a rendering or virtualization bug specific to the full-page review UI.

### 8. Codex Diff shows "Oops, an error has occurred" in VS Code
**#35481** — 6 comments, 31 👍 — [Link](https://github.com/openai/codex/issues/35481)

Another VS Code diff-view failure on Windows (extension 26.721.41059). With 31 👍 in just a few days, this appears to be a broader Windows extension regression.

### 9. gpt-5.6-luna is marked as MultiAgent V1, so V2 `spawn_agent` rejects it
**#35097** — 6 comments, 13 👍 — [Link](https://github.com/openai/codex/issues/35097)

A model metadata mismatch: `gpt-5.6-luna` is flagged as MultiAgent V1, so V2 `spawn_agent` calls reject it. A metadata/plumbing bug, but it breaks subagent workflows for Pro 20x users.

### 10. New GPT SOL 5.6 is unfair for Plus users
**#36213** — 5 comments — [Link](https://github.com/openai/codex/issues/36213)

Plus users report ~30% less usable quota under GPT SOL 5.6, requesting either a 2× usage increase or separate rate limits for smaller models. Rate-limit frustration is a recurring theme but this one has a specific, actionable ask.

---

## 4. Key PR Progress

### 1. Run code mode exclusively through the standalone host
**#36217** (merged) — [Link](https://github.com/openai/codex/pull/36217)

Moves the V8 implementation into a dedicated `codex-code-mode-runtime` crate used by `codex-code-mode-host`, removing the embedded fallback from the Codex process. Cleaner architecture, fewer runtime paths.

### 2. Precompute app-server protocol exports
**#36212** (merged) — [Link](https://github.com/openai/codex/pull/36212)

Embeds compressed stable and experimental TypeScript/JSON schema exports, removing the need for `ts-rs`/`schemars` in normal build pipelines. Faster, simpler builds.

### 3. Avoid shifting bytes in streaming output buffers
**#36194** (merged) — [Link](https://github.com/openai/codex/pull/36194)

Fixes O(n²) behavior in streaming output buffers by avoiding repeated `Vec` prefix removal when streams contain invalid UTF-8 or many framed messages. Pure performance win.

### 4. Record normalized sandbox violation events
**#36207** (merged) — [Link](https://github.com/openai/codex/pull/36207)

Unifies filesystem denials and managed-network blocks into one structured event shape, so downstream consumers no longer need to parse backend-specific output.

### 5. Coalesce concurrent remote metadata requests
**#36184** (merged) — [Link](https://github.com/openai/codex/pull/36184)

Shares in-flight `fs/getMetadata` RPCs across concurrent callers for the same path, eliminating duplicate RPCs on remote filesystems.

### 6. Make thread history projection resilient to malformed rollouts
**#36188** (merged) — [Link](https://github.com/openai/codex/pull/36188)

Fixes a checkpoint-ordinal desync that could prevent history projection after a failed rollout append followed by a valid retry. Directly addresses `#35647`-adjacent storage/history concerns.

### 7. Expose connector candidates in external agent detection
**#36218** (merged) — [Link](https://github.com/openai/codex/pull/36218)

Adds a `connectors` array to `ExternalAgentConfigDetectResponse` with candidate names, session counts, and detection sources (MCP server config, session inference).

### 8. Refresh precomputed app-server protocol exports
**#36239** (merged) — [Link](https://github.com/openai/codex/pull/36239)

Follow-up to #36212, adding connector candidates to detection responses, `enterprise_cbp_automation` plan type, and `LegacyAppPathString` usage.

### 9. Support Enterprise automation account plans
**#36228** (merged) — [Link](https://github.com/openai/codex/pull/36228)

Adds recognition for `enterprise_cbp_automation` across authentication, backend responses, and rate-limit APIs, displayed as "Enterprise (Automation)". Enables automated enterprise workflows.

### 10. Enable parallel tool calls for Codex Apps
**#31591** (open) — [Link](https://github.com/openai/codex/pull/31591)

Adds a disabled-by-default `codex_apps_parallel_tool_calls` feature that opts the host-owned `codex_apps` MCP server into parallel tool calls, preserving serial behavior for user-configured servers. Performance upside for Apps-based workflows.

---

## 5. Feature Request Trends

1. **MCP interoperability with non-OpenAI providers** — The top community ask. Users want MCP namespaces flattened or translated for Ollama, LM Studio, OpenRouter, and AWS Bedrock. File as `#26234`; expect ongoing pressure here.

2. **Fairer rate limits for Plus users** — Multiple threads (#36213 and others) push for either higher Plus quotas or separate limits on smaller models, especially now that GPT SOL 5.6 is the default.

3. **Session/thread lifecycle improvements** — Requests include reopening closed side chats (#27716), cross-device workspace continuity (#34804), and preventing reasoning-level resets after delegation (#26930). Users want sessions to be first-class, persistent, and resumable.

4. **VS Code notification integration** — Users want Codex to surface notifications through VS Code's native UI (#26555), particularly for multi-window workflows.

5. **Sandbox and shell execution reliability on Windows** — Multiple requests and bug reports center on the sandboxed shell failing on Windows (incorrect logon semantics, corrupted dependency bundles, split writable roots). Enforcement and diagnostic improvements are eagerly awaited.

---

## 6. Developer Pain Points

- **Windows is the wild west.** The majority of high-comment issues are Windows-specific: app crashes (`#32683`), spellcheck failures (`#26478`), sandbox failures (`#18620`, `#35803`, `#35864`), diff-view crashes (`#35362`, `#35481`), and OneDrive/stream disconnects (`#35420`). Windows parity is clearly the #1 reliability gap.

- **Auth friction.** OAuth issuer validation failures (#31573) and MCP login failures (#13200) suggest authentication remains fragile, especially for free/enterprise tiers.

- **Subagent and model metadata mismatches.** Issues like `#35097` (luna flagged as MultiAgent V1) and `#34821` (evicted subagents resuming with parent model) indicate that the MultiAgent V2 rollout is still rough around the edges.

- **Session storage amplification.** Forked threads writing full parent rollouts into child JSONL (`#35647`) and desktop compaction embedding full base64 images (`#23257`) point to real disk-growth concerns for long-lived sessions.

- **Rate-limit economics.** Plus users feel squeezed by model defaults they can't control, and the community is vocal about it. Expect continued pressure for transparent, fair usage policies.

---

*Digest generated from openai/codex activity between 2026-07-30 and 2026-07-31.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-31

## Today's Highlights
A new nightly release (`v0.55.0-nightly.20260730`) is available, though it contains only changelog backfills and a version bump. The maintainer team remains heads-down on two critical **P1** bugs: subagent recovery falsely reporting **GOAL success** after hitting `MAX_TURNS` (#22323), and the **generalist agent hanging indefinitely** on simple tasks (#21409) — both pending retesting. On the PR front, a wave of maintenance and security fixes landed, headlined by a fix to stop recursive glob searches on diff hunk markers (#28581) and upgrades away from EOL Node 20 in Dockerfiles.

## Releases
- **[v0.55.0-nightly.20260730.gdc859e8e4](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-nightly.20260730.gdc859e8e4)**: No functional changes — includes changelog backfills for v0.54.0-preview.0 and v0.53.0, plus a version bump to `0.55.0-nightly.20260729`.

## Hot Issues (Top 10)
1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — *P1, area/agent, 12 comments*. The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit `MAX_TURNS` before doing any analysis. This masks real failures and erodes trust in agent output. Marked `need-retesting`.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** — *P1, area/agent, 8 comments, 8 👍*. The most upvoted open issue. `gemini-cli` hangs for up to an hour on trivial tasks (e.g., folder creation) when deferring to the generalist agent. Community workaround: instruct the model not to use subagents. Maintainers have it in retest.

3. **[#25166 — Shell command execution stuck at "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** — *P1, area/core, 4 comments, 3 👍*. After simple CLI commands complete, the terminal hangs showing "Awaiting user input." Reproducible with trivial commands that never prompt — a major UX blocker for automation.

4. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — *P1, area/agent, 4 comments, 1 👍*. Browser agent crashes on Wayland sessions with `Termination Reason: GOAL` but no useful output. Environment-specific but affects a growing Linux user base.

5. **[#22186 — get-shit-done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)** — *P1, area/agent, 3 comments*. Crashes reproducibly when the GSD hook is almost finished printing the user summary. Interrupts the final deliverable step.

6. **[#24353 — Robust component level evaluations (EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)** — *P1, area/agent, 7 comments*. Epic tracking expansion of behavioral evals from 76 tests to full component-level coverage across 6 Gemini models. Signals a push for stronger regression safety.

7. **[#24246 — 400 error with >128 tools enabled](https://github.com/google-gemini/gemini-cli/issues/24246)** — *P2, area/agent, 3 comments*. Hitting a 400 error when more than ~128 (or 400) tools are available; the agent does not scope tools by enabled set. Users with many MCP servers are directly impacted.

8. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — *P2, area/agent, 5 comments*. The extraction agent re-surfaces low-signal sessions forever because only successful `read_file` marks a session as processed. Causes repeated, wasteful memory churn.

9. **[#26525 — Add deterministic redaction for Auto Memory](https://github.com/google-gemini/gemini-cli/issues/26525)** — *P2, area/security, 4 comments*. Auto Memory sends local transcript content to the model *before* redacting secrets, and logging may leak skill names. Security-focused follow-up to the memory feature.

10. **[#22465 — Stuck at interactive prompt creating Vite app](https://github.com/google-gemini/gemini-cli/issues/22465)** — *P2, area/agent, 2 comments*. The agent hangs at `npm create vite` interactive prompts instead of bypassing them. Maintainers propose a behavioral eval; community workaround is explicit `--yes` flags.

## Key PR Progress (Top 10)
1. **[#28581 — Skip diff hunk markers during @-file processing](https://github.com/google-gemini/gemini-cli/pull/28581)** — Stops unified/combined diff hunk markers from being parsed as `@file` refs, eliminating two recursive glob searches per hunk. Fixes `minimatch`/`path-scurry` heap growth on large diffs — a meaningful performance win.

2. **[#28566 — Propagate InvalidStreamError details to UI](https://github.com/google-gemini/gemini-cli/pull/28566)** — Surfaces specific stream error type/message to CLI tips, including recommending `/compress` on empty responses. Directly targets a common user confusion point.

3. **[#28481 — Refresh MCP OAuth tokens with stored client ID](https://github.com/google-gemini/gemini-cli/pull/28481)** — Fixes token refresh failures for OAuth-discovered MCP servers; previously the failure deleted stored credentials, forcing re-auth every session.

4. **[#28599 — Classify capacity exhaustion as terminal (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/28599)** — Treats `MODEL_CAPACITY_EXHAUSTED` (HTTP 429) as terminal when no retry delay is given, immediately triggering fallback instead of hanging. 

5. **[#28603 — Upgrade sandbox Dockerfile to Node 22](https://github.com/google-gemini/gemini-cli/pull/28603)** — Resolves #28584; Node 20 reached EOL 2026-04-30. Critical security hygiene for the sandbox that runs model-directed commands.

6. **[#28602 — Update Docker base image to node:24-slim](https://github.com/google-gemini/gemini-cli/pull/28602)** — Follow-up to #28603; updates the runtime base and fixes a stage copy issue for generated CLI packages.

7. **[#28596 — Add `--list-all-sessions` option](https://github.com/google-gemini/gemini-cli/pull/28596)** — Community-requested feature; lists sessions across all registered workspaces, grouped by path. Solves "I forgot which folder I created this session in."

8. **[#28597 — Load env vars before resolving settings placeholders](https://github.com/google-gemini/gemini-cli/pull/28597)** — Fixes a load-order race: `.env` was loaded *after* settings placeholders were already expanded against `process.env`, breaking `${VAR}` in configs.

9. **[#28592 — Keep Auto model visible without preview access](https://github.com/google-gemini/gemini-cli/pull/28592)** — Auto can resolve to stable models even without preview access, so hiding it based on preview metadata incorrectly removes a valid choice from `/model`.

10. **[#28551 — Fall back to embedded macOS seatbelt profiles](https://github.com/google-gemini/gemini-cli/pull/28551)** — Fixes critical startup crash on macOS/gMac when static `.sb` profiles are missing, enabling `-s` sandbox mode to work.

## Feature Request Trends
- **Agent self-awareness & transparency**: Multiple requests for the CLI to understand its own flags/hotkeys (#21432), surface subagent trajectories via `/chat share` (#22598), and include subagent context in `/bug` reports (#21763). Users want to see *why* the agent acted, not just what it did.
- **Automatic context management**: Strong push for auto-compression on context overflow (#28488) and clearer guidance on empty/truncated responses (#28566) — users want the tool to self-heal context limits instead of hard-stopping.
- **Proactive safety guardrails**: Requests for the agent to avoid destructive git/DB commands (#22672) and to stop creating tmp scripts in random directories (#23571). Users want deterministic, reviewable behavior.
- **Session/task management**: Cross-workspace session listing (#28596) and better memory hygiene (quarantine invalid patches, #26523; stop low-signal retries, #26522) show demand for lifecycle tooling.

## Developer Pain Points
- **Hangs and false "success" are the #1 frustration**: The combination of subagent MAX_TURNS being reported as GOAL success (#22323), generalist hangs (#21409), and post-command "Waiting input" freezes (#25166) erodes trust in automation. Users are forced to disable subagents entirely as a workaround — a blunt instrument.
- **Configuration is silently ignored**: Browser agent ignores `settings.json` overrides (#22267) and subagents run despite "disabled" configs (#22093). Configuration that doesn't behave as documented creates safety and predictability concerns.
- **EOL/runtime churn**: Node 20 EOL (2026-04-30) required urgent Dockerfile fixes (#28602, #28603) — but also signals that the project needs proactive dependency lifecycle tracking to avoid last-minute security scrambles.
- **Scale-related failures**: 400 errors with >128 tools (#24246) and heap growth on large diff prompts (#28581) show the CLI straining at the edges of large MCP setups and big diffs — the cost of extensibility without bounds.

---
*Data window: 2026-07-30 00:00 UTC → 2026-07-31 00:00 UTC*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-31

## Today's Highlights
v1.0.77 ships with a new browser-based OAuth login flow (now default for local terminals) and unconditional autopilot approval now properly bypasses the sandbox. The community is actively reporting issues around AI credit consumption visibility, sub-agent reliability with full tool access, and a critical regression in v1.0.74/1.0.76 affecting exit screens and command handling.

## Releases
**[v1.0.77](https://github.com/github/copilot-cli/releases/tag/v1.0.77)** — 2026-07-30
- Unconditional autopilot approval now disables sandbox for the current session when bypass is allowed
- Ctrl+G now opens your editor to edit `ask_user` freeform answers without closing the prompt
- Added a **browser-based (web) OAuth login flow**, now the default for `copilot login` on local interactive terminals; device code remains default on remote/headless terminals
- Use `--web-flow`/`--device-code` to force a mode, or pick one in the interactive `/login` command

*Note: v1.0.77-0 (pre-release) contains the same OAuth additions.*

## Hot Issues

1. **[#3767 — Oversized attachment permanently wedges session](https://github.com/github/copilot-cli/issues/3767)** [CLOSED]  
   Attachments over CAPI's 5MB native limit cause a hard failure with no recovery path. This long-running issue (June → July) had 13 comments and is now closed, but remains a cautionary tale for large-file workflows.

2. **[#4295 — AI Credits Near-Limit Warning](https://github.com/github/copilot-cli/issues/4295)**  
   Feature parity request: VS 2026 Professional warns users when nearing their AI Credits limit; CLI users want the same visibility. The community is actively discussing this (8 comments).

3. **[#1381 — Rewind requires git repository](https://github.com/github/copilot-cli/issues/1381)** [10 👍]  
   Users of non-git VCS (e.g., Jujutsu) cannot use the Rewind feature. High community demand (10 upvotes) for decoupling Rewind from git detection.

4. **[#4308 & #4309 — Sessions continue consuming credits after tasks complete](https://github.com/github/copilot-cli/issues/4308)**  
   Two separate reports (nearly identical) that interactive sessions consumed ~97.8% of AI credits after all visible work was done. Both in triage; suggests a possible background agent or compaction loop.

5. **[#4293 — Sub-agents with full tool access return empty](https://github.com/github/copilot-cli/issues/4293)**  
   Sub-agents launched via `task` tool silently return **no response** when the agent type has full tool access; restricted-tool agents work fine. No error, no log — a difficult-to-debug failure mode.

6. **[#4305 — "Failed to convert JavaScript value 'Undefined' into rust type 'String'"](https://github.com/github/copilot-cli/issues/4305)** [CLOSED]  
   Regression in v1.0.76 where `/model auto` and nearly any command triggers a Rust/JS binding error. Quickly closed, but indicates a potential API compatibility issue with provider responses.

7. **[#4310 — Fallback to 128K token budget for large-context models](https://github.com/github/copilot-cli/issues/4310)**  
   When a routed model reports no capability limits, the engine silently falls back to a hardcoded 128K token budget — even for 1M-token models. Will cause premature context compaction for large-context providers.

8. **[#4299 — Increasing typing latency over long sessions](https://github.com/github/copilot-cli/issues/4299)**  
   Long-running sessions (especially with background agents) become progressively laggy to type in, making the CLI unusable. Highlights a likely event-loop or rendering bottleneck.

9. **[#4306 — Subtasks freeze and stop responding](https://github.com/github/copilot-cli/issues/4306)**  
   In autopilot mode with `/fleet` loops, subtasks freeze mid-session with no error. Similar to #4293 — suggests a broader agent orchestration instability.

10. **[#4304 — Session sidebar cannot be navigated with arrow keys](https://github.com/github/copilot-cli/issues/4304)**  
   UI regression: the new session sidebar ignores arrow-key navigation. Minor but impacts daily workflow for keyboard-driven users.

## Key PR Progress
*No pull requests were updated in the last 24 hours.* (Data source returned 0 items.)

## Feature Request Trends

1. **AI Credit Transparency** (#4295, #4308, #4309) — Users want proactive warnings before hitting credit limits, plus better visibility into what consumes credits (especially background tasks).
2. **Non-git VCS Support** (#1381) — Growing demand to decouple Rewind from git, accommodating Jujutsu and other VCS tools.
3. **Selective Sandbox Tool Control** (#4298) — Admins want fine-grained control over which bundled tools run inside the sandbox (allowlists), not just blanket enable/disable.
4. **Bearer Token / Custom Broker Auth** (#4300) — Corporate environments with key-based auth disabled need bearer-token support or a customizable broker for automated CI/CD runs.
5. **Login Flow Flexibility** (from v1.0.77 release) — Web-flow OAuth is now default, but users still want forceable device-code mode for remote/headless environments.

## Developer Pain Points

- **Silent Agent Failures** (#4293, #4306): Sub-agents returning empty or freezing without error messages is the most frustrating pattern — no logs, no partial output, just nothing. Debugging is nearly impossible.
- **Credit Drain Without Visibility** (#4308, #4309): Sessions appearing "done" but continuing to consume AI credits erodes trust in cost predictability.
- **Latency Degradation** (#4299): Typing lag that worsens over long sessions disrupts the primary interaction model of the CLI.
- **Config/Environment Fragility** (#4297, #4303): Crashes on non-default log levels, and MCP server misconfigurations breaking sub-agents entirely, make the tool feel brittle in complex setups.
- **Terminal/Platform Inconsistencies** (#4296, #2841, #4294): Paste issues in iTerm2, mouse scroll failures over SSH (MobaXterm), and `COLORTERM` injection on session resume show terminal-compat is still an uneven experience.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-07-31**

---

## Today's Highlights

The community is experiencing significant turbulence this week: a critical **429 rate-limiting outage** (#2571) is preventing many users from accessing the CLI entirely, while a newly reported **intermittent freezes** bug (#2570) affecting Windows users correlates mysteriously with browser tab state. On the development front, a valuable PR (#2565) fixing a subtle Python memory-management issue in hook triggers has just landed, underscoring the project's active maintenance. Meanwhile, the long-standing **Memory System** feature request (#1283) continues to gain traction as the highest-value enhancement on the roadmap.

---

## Releases

No new releases were published in the last 24 hours.

---

## Hot Issues

### #2571 — [bug] LLM Overloaded! Can't use Kimi at all
**Author:** andrew-sz | **Created:** 2026-07-30 | **Comments:** 1 | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2571)
A **critical availability issue** where the provider returns HTTP 429 (rate limit exceeded) despite the user being on a paid subscription. This is a blocking issue affecting core functionality, and with only one comment so far, the community and maintainers are still assessing the scale of the outage. **Why it matters:** If widespread, this erodes trust in paid tiers.

### #2570 — [bug] CLI intermittently freezes with spinning moon; correlated with browser tab state
**Author:** XbackMK | **Created:** 2026-07-30 | **Comments:** 0 | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2570)
A **confusing Windows-specific bug** where the CLI becomes unresponsive, and the freeze timing appears linked to browser tab activity. The mechanism is unclear (possible resource contention, event-loop blocking, or rendering issue). Zero comments means no troubleshooting has begun yet. This is a **high-priority reproducibility challenge** for the dev team.

### #1283 — [enhancement] Feature Request: Memory System — Persistent context across sessions
**Author:** CatKang | **Created:** 2026-02-27 | **Updated:** 2026-07-30 | **Comments:** 7 | [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1283)
The **most discussed open feature request** in the project. Proposes a dual-mode memory system: automatic (AI-managed notes) and manual (user-defined persistent instructions). This would allow the CLI to remember project patterns and user preferences indefinitely. **Why it matters:** This is the #1 differentiator users want—turning Kimi from a stateless tool into a long-term development companion.

---

## Key PR Progress

### #2565 — [fix] fix(hooks): keep a strong reference to fire-and-forget hook triggers
**Author:** LHMQ878 | **Updated:** 2026-07-30 | [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2565)
A subtle but **critical fix** for a Python garbage-collection issue. `asyncio` holds tasks weakly, so a fire-and-forget hook trigger could be garbage-collected mid-execution. This PR keeps a strong reference, preventing flaky or dropped hook executions. Directly fixes #2564.

---

## Feature Request Trends

Distilling all open issues, the community's most requested feature directions are:

- **Persistent Memory & Context (#1283):** The ability to retain project knowledge, user preferences, and instructions across sessions—both manual and AI-managed. This is the most-reviewed and highest-community-interest issue.
- **Reliability & Stability (Implied):** While not a formal feature request, the flood of 429 errors and freeze bugs indicates a strong underlying demand for robust provider error handling and performance under load.

---

## Developer Pain Points

Recurring frustrations based on recent issue frequency:

1. **Provider Rate-Limiting Outages (#2571):** A single 429 response taking down the entire CLI experience is a major pain point—especially for users on paid plans who expect capacity guarantees.
2. **Unpredictable Freezing (#2570):** The "spinning moon" freeze is particularly frustrating because it is intermittent and appears linked to unrelated system activity (browser tabs), making it hard to reproduce and thus hard to work around.
3. **Scope of Impact:** Both critical bugs are affecting users across different platforms (macOS and Windows) and different subscription tiers, suggesting possible systemic issues rather than isolated configurations.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-31

## Today's Highlights

OpenCode v1.18.10 shipped with automatic Modal model discovery and a round of desktop UI polish, but the community's attention is firmly on the new tabbed interface: a "Stale read from <Show>" crash (#39704) affecting session switching is already being addressed in PR #39767. Meanwhile, contributor kitlangton continues to dominate the TUI front, landing a streak of PRs that add hot-reload, an open menu, and session directory inheritance.

## Releases

**v1.18.10** — The release focuses on the desktop app with quality-of-life improvements:
- **Core**: Automatic discovery of available Modal models (@devennavani)
- **Desktop**: Duplicate attachment prevention, persistent new-session button, improved toast stacking/dismissal/mobile layout, refined tab hover states

## Hot Issues

1. **[#39653 — GPT-5.6 Sol, server overloaded errors](https://github.com/anomalyco/opencode/issues/39653)** — 16 comments, 10 👍
   Users report repeated "server overloaded" errors with Sol while Pi and Codex work fine. This is the highest-traffic issue of the day, indicating a prominent provider-side problem that is drawing substantial community attention.

2. **[#37762 — Problems With Responses](https://github.com/anomalyco/opencode/issues/37762)** — 8 comments
   An Ollama user with 64GB RAM and 4GB VRAM struggles with email preparation. The issue highlights the ongoing challenge of local model performance and configuration for users migrating from cloud models.

3. **[#39288 — opencode Error after upgrade to 1.18.8](https://github.com/anomalyco/opencode/issues/39288)** — 6 comments
   `Error: AutoScroller plugin depends on Scroller plugin` — a plugin dependency resolution failure plaguing desktop users after upgrade.

4. **[#38655 — Can't switch between plan and build after update](https://github.com/anomalyco/opencode/issues/38655)** — 5 comments
   Mode switching is broken; build is forced as default. The issue is not accompanied by plugin details, making diagnosis harder for maintainers.

5. **[#37628 — npm install -g opencode-ai gets 16bit issue](https://github.com/anomalyco/opencode/issues/37628)** — 5 comments
   Windows users with Node v26.5.0 hit an executable compatibility error — a recurring Windows packaging/release issue.

6. **[#37579 — 问题长时间没有任何响应 (No response for a long time)](https://github.com/anomalyco/opencode/issues/37579)** — 5 comments
   A Chinese-language report of unresponsive behavior, including logs. Billing frustration ("花钱用不了" — "paid but can't use") echoes in this thread.

7. **[#39256 — [FEATURE]: Clarify `variants` sub-config case conventions](https://github.com/anomalyco/opencode/issues/39256)** — 4 comments
   Users want explicit documentation on whether `variants` sub-configurations use camelCase or snake_case — a small but impactful documentation gap.

8. **[#39491 — Plan mode can write and edit files via bash](https://github.com/anomalyco/opencode/issues/39491)** — 4 comments
   Claude Sonnet 4.6 in plan mode bypassed the write-tool restriction by using bash (`cat > file`). This is a **security-relevant** mode-escaping bug.

9. **[#27837 — Web UI: session list empty in web server mode](https://github.com/anomalyco/opencode/issues/27837)** — 4 comments, 2 👍
   A long-standing (May) bug where the web UI session list is empty despite `/api/session` returning data. The reporter included a root-cause analysis, but the issue remains open in v1.18.x.

10. **[#39655 — Web shows "No folders found"](https://github.com/anomalyco/opencode/issues/39655)** — 4 comments
    Web UI fails to display projects even though the backend API returns them correctly — a frontend/backend integration bug.

## Key PR Progress

1. **[#39767 — fix(app): prevent stale session tab reads](https://github.com/anomalyco/opencode/pull/39767)** — Closes #39766 and #39704. Fixes the "Stale read from <Show>" crash during session/project navigation when Solid transitions away from the previous UI tree. This one directly addresses today's top crash report.

2. **[#39776 — feat(tui): hot-reload local TUI plugins](https://github.com/anomalyco/opencode/pull/39776)** — Editing a local TUI plugin now takes effect without restarting the client — the TUI half now matches core/backend plugin hot-reload behavior.

3. **[#39752 — feat(tui): add open menu for sessions and projects](https://github.com/anomalyco/opencode/pull/39752)** — Adds `ctrl+o` open menu to v2 TUI for jumping between recent sessions across projects, replacing the projects-only dialog.

4. **[#39753 — feat(tui): inherit session directory when creating a new session](https://github.com/anomalyco/opencode/pull/39753)** — `/new` in v2 TUI now inherits the previous session's project directory, matching desktop's new-tab behavior.

5. **[#39748 — fix(session): retry failed title generation](https://github.com/anomalyco/opencode/pull/39748)** — Automatic title generation retries after a failed first step and preserves the session's original user prompt. Closes #39529.

6. **[#39747 — feat(session): make generated titles optional](https://github.com/anomalyco/opencode/pull/39747)** — Sessions remain genuinely untitled until auto-generation succeeds or a user manually renames; API contracts updated to omit `title` when absent.

7. **[#39781 — feat(app): select base branch for new workspaces](https://github.com/anomalyco/opencode/pull/39781)** — Closes #39778/#39779. Fixes `git worktree add` using no start point; lets users pick a base branch when creating workspaces.

8. **[#39764 — feat(plugin): add session request hook](https://github.com/anomalyco/opencode/pull/39764)** — Exposes `session.request` on plugin boundaries, letting plugins mutate outgoing HTTP headers and serialized request bodies after authentication.

9. **[#39780 — fix(tui): clarify open menu project labels](https://github.com/anomalyco/opencode/pull/39780)** — Improves project identity in the TUI Open dialog: concise project names on the left, subdued paths on the right, session age shown only when no project exists.

10. **[#39774 — fix(tui): preserve current selection across list updates](https://github.com/anomalyco/opencode/pull/39774)** — Fixes the session picker showing the current-session dot on one row while Enter selects a different blue-highlighted row after async updates.

## Feature Request Trends

- **Local & self-hosted model support** — There is a persistent demand for better local LLM integration, ranging from [LAN provider discovery](https://github.com/anomalyco/opencode/pull/27554) to complaints about Ollama and oMLX connectivity. Users want OpenCode to treat local servers as first-class providers.
- **LiteLLM proxy as a built-in provider** ([#29935](https://github.com/anomalyco/opencode/issues/29935)) — This long-running request (May, 3 comments, 5 👍) continues to surface: users want unified access to 100+ providers via LiteLLM's OpenAI-compatible proxy without custom configuration.
- **Documentation clarifications** — With the `variants` case-convention question ([#39256](https://github.com/anomalyco/opencode/issues/39256)) and French translation errors ([#38498](https://github.com/anomalyco/opencode/issues/38498)), the community is pushing for higher-quality, more precise docs.
- **Faster failure on network errors** ([#39771](https://github.com/anomalyco/opencode/issues/39771)) — Users in constrained networks (e.g., China) want configurable timeouts and fallback behavior instead of the default 60–120s hang.

## Developer Pain Points

- **Mode/feature regressions after updates** — The plan/build mode switch regression ([#38655](https://github.com/anomalyco/opencode/issues/38655)), plugin dependency errors after upgrade ([#39288](https://github.com/anomalyco/opencode/issues/39288)), and crash-on-session-switch ([#39704](https://github.com/anomalyco/opencode/issues/39704)) all suggest integration-test gaps that ship in releases.
- **Plan mode escapability** ([#39491](https://github.com/anomalyco/opencode/issues/39491)) — The fact that a model can write files via bash while in read-only plan mode is a recurring security/UX concern; the community expects strict tool enforcement.
- **Windows release quality** — Multiple unresolved Windows-specific problems, including 16-bit compatibility errors ([#37628](https://github.com/anomalyco/opencode/issues/37628)), corrupted executables ([#37566](https://github.com/anomalyco/opencode/issues/37566)), and OS-reserved keybindings ([#38585](https://github.com/anomalyco/opencode/issues/38585)), indicate an ongoing Windows packaging stability issue.
- **Provider reliability and billing transparency** — Reports of "server overloaded" (Sol, [#39653](https://github.com/anomalyco/opencode/issues/39653)), blocked paid-model requests via OpenCode Go ([#38473](https://github.com/anomalyco/opencode/issues/38473)), and unclear token accounting ([#37748](https://github.com/anomalyco/opencode/issues/37748)) show that users are sensitive to both reliability and how their credits are reported.
- **Web UI integration gaps** — The empty session list ([#27837](https://github.com/anomalyco/opencode/issues/27837)) and "No folders found" ([#39655](https://github.com/anomalyco/opencode/issues/39655)) are two separate manifestations of the same theme: the web frontend lags the API and desktop in maturity.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-31

## Today's Highlights
This week's activity centers on protocol work and TUI stability: a new transport-neutral session protocol package (`@earendil-works/pi-protocol`) landed, alongside clipboard and grapheme width fixes for Linux/Wayland users. Provider integration updates continue across Anthropic OAuth handling, OpenAI background mode, and Gemini 3.x tool-call ID preservation. Several core issues remain unresolved, most notably stalled model-catalog promises permanently wedging availability and login flows.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[OpenAI Responses: stateful continuation and server-side compaction](https://github.com/earendil-works/pi/issues/7317)** — Pi's Responses adapter replays full session history after each tool result instead of leveraging `previous_response_id` or server-side compaction. Significant for long, tool-heavy GPT runs; community interest shown with 1 👍.

2. **[Stalled availability refresh permanently wedges ModelRuntime](https://github.com/earendil-works/pi/issues/7301)** — `forceRefreshAvailability()` chains onto a stuck promise, so the runtime never recovers even after the root cause clears. A critical reliability gap that also causes the related `/scoped-models` hang (#7153) and `/login` stall (#7027).

3. **[Anthropic stream parser discards initial block](https://github.com/earendil-works/pi/issues/7283)** — The parser assumes content-block start events are empty, but some Anthropic responses include content in the initial event. Small fix with outsized impact on first-part reliability. In progress.

4. **[Gemini 3.x tool-call IDs stripped](https://github.com/earendil-works/pi/issues/7047)** — `id` fields are dropped from `functionCall`/`functionResponse` parts during history replay, breaking multi-turn tool conversations on Gemini 3. Affects providers using the `google-generative-ai` SDK. 1 👍.

5. **[`anthropic-messages` never sends `x-client-request-id`](https://github.com/earendil-works/pi/issues/7161)** — Unlike OpenAI paths, Anthropic lacks the session-affinity header, breaking gateways that round-robin between accounts. Open with 6 comments.

6. **[Wayland Ctrl+V paste silently fails](https://github.com/earendil-works/pi/issues/7248)** — `readClipboardText()` uses an X11-only addon; on Wayland sessions the clipboard is empty or stale. Now fixed by PR #7261 (wl-paste/xclip fallback), but the issue highlights broader Linux desktop support gaps.

7. **[Full re-render every 1s with offscreen tool cards](https://github.com/earendil-works/pi/issues/7194)** — When a tool card scrolls outside the viewport, Pi re-paints the entire session transcript every second. Particularly painful for remote sandbox users; closed after 7 comments.

8. **[Windows: input line redrawn on every keystroke](https://github.com/earendil-works/pi/issues/6300)** — Each character appears on a new line in cmd.exe and Windows Terminal. Long-standing (since July 4), 6 comments, still open.

9. **[/scoped-models stalls ~5 minutes on catalog refresh](https://github.com/earendil-works/pi/issues/7153)** — The command blocks synchronously on model-catalog refresh before rendering any UI or loading state. Related to the same stuck-promise root cause as #7301. 1 👍.

10. **[API-key login can hang after saving credential](https://github.com/earendil-works/pi/issues/7027)** — `/login openrouter` leaves the TUI stuck when model-catalog refresh stalls, even though credentials are already persisted to `auth.json`. 4 👍 — highest community agreement in this batch.

## Key PR Progress

1. **[feat(protocol): add remote session wire protocol](https://github.com/earendil-works/pi/pull/7344)** — New `@earendil-works/pi-protocol` package with validated commands, events, snapshots, and strict bounded CBOR encoding + length-prefixed framing. Foundation for remote session support.

2. **[feat(client): add runtime-neutral session client](https://github.com/earendil-works/pi/pull/7348)** — Transport-neutral `@earendil-works/pi-client` with connection lifecycle as a discriminated union, request correlation, and multi-session handles.

3. **[fix(coding-agent): share host modules with native esm extensions](https://github.com/earendil-works/pi/pull/7011)** — Intercepts native imports so ESM extensions reuse host Pi modules instead of resolving private copies, preventing module state divergence. In progress.

4. **[feat(coding-agent): Experimental loadout management](https://github.com/earendil-works/pi/pull/7148)** — `/loadout` to enable/disable extensions mid-session, with persisted overrides restored on resumption. Draft from mitsuhiko.

5. **[fix: custom-compaction through provider via new model runtime](https://github.com/earendil-works/pi/pull/7325)** — Fixes provider-registered models being visible in the runtime registry but undispatchable via compat `complete()`. Addresses #7273.

6. **[openai background mode responses](https://github.com/earendil-works/pi/pull/7339)** — Initial implementation of OpenAI's `background: true` mode. Draft; author requests design feedback.

7. **[feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216)** — Uses OpenAI's Bedrock provider under the hood. Supersedes an earlier attempt; open since July 1.

8. **[fix: formatting of delta content blocks](https://github.com/earendil-works/pi/pull/7216)** — Fixes `[object Object]` stringification when providers stream `choice.delta.content` as typed arrays. In progress.

9. **[fix(tui): align grapheme widths with terminal cells](https://github.com/earendil-works/pi/pull/6987)** — Improves cell-width estimation; addresses rendering issues for wide/zero-width characters. Closed (merged or superseded).

10. **[fix(code-agent): read clipboard via wl-paste on Wayland](https://github.com/earendil-works/pi/pull/7261)** — Falls back to `wl-paste`/`xclip`/`xsel` on Linux, mirroring the copy path. Direct fix for #7248.

## Feature Request Trends
- **Remote session support**: Multiple PRs add a wire protocol and runtime-neutral client — a clear push toward headless/remote Pi sessions with reconnection.
- **Provider parity**: Requests for OpenAI `background: true`, Bedrock Mantle, and stateful Responses continuation show demand for richer provider API usage and reduced transcript replay.
- **Session lifecycle**: `/loadout` management and explicit `AgentHarness.shutdown()` point toward better mid-session control and clean teardown.
- **Better default diagnostics**: Users want `version` to include runtime (bun/node/deno) to simplify bug triage; README installation instructions are also requested for onboarding.

## Developer Pain Points
- **Stuck-promise cascades**: Model-catalog/availability refreshes that never settle permanently break `/scoped-models`, `/login`, and `getAvailable()` — with no timeout or user feedback. The highest-signal reliability complaint this week (4 issues trace to it).
- **Unicode/grapheme rendering**: Devanagari text breaks the TUI; Windows input redraws per keystroke. Terminal rendering remains the most fragile cross-platform area.
- **Silent failures**: Wayland clipboard paste, Fireworks instant timeouts with no cause, and Anthropic stream-discarded content blocks all fail without clear diagnostics.
- **Provider hardcoding**: OAuth-token detection hardcoded to `sk-ant-oat` and missing request IDs frustrate gateway/proxy users; non-standard streaming responses from Databricks/Fireworks models hit by multiple issues.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-31

## Today's Highlights

The project is in a heavy stabilization and reliability push. A nightly release (v0.21.1-nightly.20260731) shipped with CI fixes, while multiple E2E test failures are being tracked and auto-fixed by the fleet system. The Anthropic converter also received significant attention, with a batch of bugs (stale thinking signatures, tool_result ordering, ID sanitization) reported and one fix PR already merged into the codebase.

---

## Releases

**v0.21.1-nightly.20260731.702932cc7** — No significant user-facing changes in this nightly. Contains CI fixes for container jobs and a fix for web-shell pre-rendering. ([View release](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.1-nightly.20260731.702932cc7))

---

## Hot Issues

1. **[#8172: Agent Team: teammate messages queue for entire duration of long multi-tool-call turn](https://github.com/QwenLM/qwen-code/issues/8172)** *(P2, new)* — Messages from teammates wait until `StreamingState.Idle`, which can be a very long time during multi-tool-call turns. Community reaction: 3 comments, noting it's a real design limitation of the Agent Team feature.

2. **[#8162: Anthropic converter: stale thinking signatures not pruned](https://github.com/QwenLM/qwen-code/issues/8162)** *(P2, new)* — After sibling tool_use blocks are removed by cleanup cycles, stale thinking blocks remain in historical turns. This is the fourth in a series of converter bugs reported by netbrah this week — pointing to a broader reliability issue in the Anthropic path.

3. **[#8136: Provider warning sanitizer truncates ports & leaks passwords containing @](https://github.com/QwenLM/qwen-code/issues/8136)** *(P2, new)* — A security-relevant bug: the sanitization logic for provider warnings misparses URLs containing `@` in passwords and truncates messages with ports. A fix PR (#8137) is already open. Community reaction: 4 comments confirming the bug and design decisions.

4. **[#8138: Worktree settings.json writes to project root instead of worktree](https://github.com/QwenLM/qwen-code/issues/8138)** *(P2, new)* — Settings changes in a git worktree persist to the global/project-root settings rather than the worktree's own `.qwen/` directory. A fix is already in PR #8152. This is a consistency issue between file ops (which respect worktrees) and settings (which don't).

5. **[#7972: 0.21.1 crashes 3 times](https://github.com/QwenLM/qwen-code/issues/7972)** *(P2, Chinese)* — User reports crashing three times on Windows after upgrade. A companion work item exists: PR #8088 adds an `uncaughtException` handler to surface the error instead of crashing silently. The investigation is ongoing with a `need-information` status.

6. **[#8146: Desktop app not working with LMStudio](https://github.com/QwenLM/qwen-code/issues/8146)** *(P2, new)* — Desktop client on Windows doesn't send anything to the LMStudio API despite showing activity. Community reaction: 4 comments; no clear root cause yet.

7. **[#4083: Core + CLI architecture review — 12 structural issues](https://github.com/QwenLM/qwen-code/issues/4063)** *(P0/P1, open since May)* — A comprehensive architecture review flagging 14 structural problems, notably the core type system being audited to `@google/genai` types across 136 files. Still open as a tracking issue but increasingly cited in design discussions.

8. **[#8159: Anthropic converter: trailing tool_use stripped when no subsequent message](https://github.com/QwenLM/qwen-code/issues/8159)** *(P2, new)* — A correctness bug in history cleanup: `cleanOrphanedToolCalls` strips trailing `tool_use` blocks that are legitimately the model's most recent output. A fix PR (#8163) is already open.

9. **[#8124: Startup banner sometimes missing top lines on first paint](https://github.com/QwenLM/qwen-code/issues/8124)** *(P2, Windows)* — Intermittent rendering issue in the TUI's startup banner on Windows with pending provider updates. External contributor dpc00 reported with detailed diagnostics.

10. **[#7923: Desktop client can't reference correct files](https://github.com/QwenLM/qwen-code/issues/8123)** *(P3, Chinese)* — Using `@` to reference files fails to find a Java file in the project directory. Possibly related to file indexing or path resolution in the desktop client.

---

## Key PR Progress

1. **[#8163: Don't strip trailing tool_use and dedup duplicate tool_result blocks](https://github.com/QwenLM/qwen-code/pull/8163)** — Fixes #8159. `cleanOrphanedToolCalls` now distinguishes "no result yet" from "orphan", preserving trailing tool_use blocks.

2. **[#8137: Scope warning credential stripping to the URL authority](https://github.com/QwenLM/qwen-code/pull/8137)** — Fixes #8136. The sanitizer now bounds credential search to the URL authority, matching the behavior of its sibling implementation, and deletes bespoke heuristics.

3. **[#8152: Isolate workspace settings and context file resolution for worktree sessions](https://github.com/QwenLM/qwen-code/pull/8152)** — Fixes #8138. ACP sessions in worktrees now resolve `settings.json` and `QWEN.md` against the worktree directory.

4. **[#8088: Prevent silent VP-mode crash by adding uncaughtException handler](https://github.com/QwenLM/qwen-code/pull/8088)** — Related to #7971, #7972, #7779, #7781. Adds error visibility in alternative-screen mode so future crashes surface diagnostics.

5. **[#8132: Package Web Shell as a release-ready desktop app](https://github.com/QwenLM/qwen-code/pull/8132)** — Turns the Tauri POC into a production desktop shell wrapping Web Shell, with workspace management and recovery states.

6. **[#8032: Add a host tool invocation guard](https://github.com/QwenLM/qwen-code/pull/8032)** — Implements a configurable in-process guard for tool calls that can intercept, observe, and potentially block tool execution — supports the trustworthy agent direction in #8102.

7. **[#8056: Isolate managed memory by selected workspace](https://github.com/QwenLM/qwen-code/pull/8056)** — Work on workspace-qualified memory operations and opt-in exact-workspace storage mode.

8. **[#8005: Adopt Goal v3 in interactive TUI](https://github.com/QwenLM/qwen-code/pull/8005)** — A large PR connecting the TUI to the Goal v3 runtime with lifecycle cards and two-lane input queue.

9. **[#8169: Add OpenAI Responses API content generator](https://github.com/QwenLM/qwen-code/pull/8169)** — New single content generator for the OpenAI Responses API — a significant addition that could improve OpenAI-compatible provider compatibility.

10. **[#8171: Configure background agent turn limits](https://github.com/QwenLM/qwen-code/pull/8171)** — Implements #8168. Adds `memory.agentMaxTurns` setting for managed dream and auto-skill review agents, unifying their existing defaults of 8 turns.

---

## Feature Request Trends

1. **Trustworthy agent runtime** ([#8102](https://github.com/QwenLM/qwen-code/issues/8102)) — Keep the language model outside the trust boundary; make the runtime deterministically constrain, authorize, and observe tool actions. Already seeing partial implementation in PR #8032's host guard.

2. **Session-to-file attribution** ([#7966](https://github.com/QwenLM/qwen-code/issues/7966)) — Users want to know which session generated which files, including indirect file writes via code execution.

3. **Agent infrastructure monitoring** ([#8128](https://github.com/QwenLM/qwen-code/issues/8128), [#7167](https://github.com/QwenLM/qwen-code/issues/7167)) — Demand for observability: per-workspace subagent status, fleet health dashboards, and status endpoints.

4. **Configurable agent limits** ([#8168](https://github.com/QwenLM/qwen-code/issues/8168)) — Make dream/background agent turn counts configurable via settings instead of hardcoded defaults.

5. **Auto-fix CI & review comments workflow** ([#4362](https://github.com/QwenLM/qwen-code/issues/4362)) — Users want an opt-in workflow that automatically fixes CI failures and addresses review comments on active PRs.

---

## Developer Pain Points

- **Anthropic converter reliability** — Five converter bugs in one week (#8159, #8160, #8161, #8162) suggest the code path is fragile under history-trimming and mixed-content conditions, causing silent data corruption in conversations.

- **Windows-specific bugs pile up** — Crashes ([#7972](https://github.com/QwenLM/qwen-code/issues/7972)), installer SHA-256 failures ([#7118](https://github.com/QwenLM/qwen-code/issues/7118)), desktop app integration ([#8146](https://github.com/QwenLM/qwen-code/issues/8146)), and rendering issues (#8124). CI portability PR #8050 signals the team is actively working on this.

- **Flaky E2E tests disrupting the main branch** — Multiple CI failures tracked by bots (#8153, #8133, #8076, #8108) around permission-control and system-control SDK tests. The community is addressing this through test-scoping fixes, but recurring flakes slow down release confidence.

- **Worktree isolation is incomplete** — Settings and context files not respecting worktree boundaries (#8138) while file operations already do, creating inconsistent behavior that confuses users in multi-tenant setups.

- **Gemini type system coupling** ([#4063](https://github.com/QwenLM/qwen-code/issues/4063)) — `@google/genai` types leak across 136 files, making architecture rigid and hindering provider extensibility — repeatedly cited in design discussions.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-31

## 1. Today's Highlights

The project has officially renamed to **CodeWhale** (v0.9.2), with the legacy `deepseek-tui` npm package deprecated and receiving no further releases. Two major refactor epic tracks are converging: the **command-boundary refactor** (#2870) is landing in mergeable layers via PR #4992, while the **v0.9.3 monolith split** (#3306) aims to break the 14,878-line `main.rs` and 6,970-line subagent module into a single-binary, library-backed architecture. Community discussion is active around compile-time pain from the TUI crate monolith (#4991) and a Chinese translation debate over "Constitution" (#4949).

## 2. Releases

**v0.9.2** — The final release under the `deepseek-tui` naming. Codewhale is now the public product from Shannon Labs; the `codewhale` command, npm package, and release assets remain lowercase technical identifiers. The legacy `deepseek-tui` npm package is deprecated with no further releases. Users migrating from v0.8.x legacy `deepseek`/`d…` commands should expect the Codewhale replacement path.

## 3. Hot Issues

1. **[#2870 — EPIC: staged command-boundary refactor](https://github.com/Hmbown/CodeWhale/issues/2870)** — Tracks the smaller mergeable layers for the command-boundary refactor. 19 comments; shows active community engagement on breaking a large refactor into reviewable chunks.

2. **[#2369 — Config paths fragmented across OS/Cygwin + silent migration bug](https://github.com/Hmbown/CodeWhale/issues/2369)** — Windows and Cygwin resolve home directories differently; a legacy migration can silently corrupt config paths. Critical for cross-platform reliability.

3. **[#4022 — CLI/TUI parity for subagent/runtime control surfaces](https://github.com/Hmbown/CodeWhale/issues/4022)** — Subagent status/cancellation lives only in the TUI sidebar; must be exposed for future cloud/remote workflows. Product-shape discussion.

4. **[#3306 — v0.9.3 Refactor: converge runtime ownership, one executable](https://github.com/Hmbown/CodeWhale/issues/3306)** — Umbrella for the monolith split: 18 Rust packages, 771k lines, 87% in `codewhale-tui`. Parallel runtime/tool/config paths must converge.

5. **[#4949 — Chinese translation of "Constitution"](https://github.com/Hmbown/CodeWhale/issues/4949)** — Community debate: "宪法" (constitution, politically sensitive) vs "协作准则" (collaboration guideline). Bilingual discussion; needs native-speaker consensus.

6. **[#4991 — Compilation times and the TUI crate monolith](https://github.com/Hmbown/CodeWhale/issues/4991)** — Opened yesterday; 1 comment. Community validation of the refactor epics: developers are feeling compile-time pain directly.

7. **[#4988 — Compaction fails before context/quota exhaustion](https://github.com/Hmbown/CodeWhale/issues/4988)** — Closed as tracked; dogfood failure where trigger cause is unproven (context headroom vs quota vs malformed transcript). Needs persistent trigger/failure receipt.

8. **[#4987 — Provider credentials: one home-scoped store](https://github.com/Hmbown/CodeWhale/issues/4987)** — Closed as tracked; `CODEWHALE_HOME` creates an isolated secret store that looks "missing" from fresh terminals. UX/reliability bug.

9. **[#4978 — Anthropic API error: 'type' must be in ["enabled","disabled","auto"]](https://github.com/Hmbown/CodeWhale/issues/4978)** — OpenModel (Anthropic-compatible) provider gets HTTP 400 intermittently. Chinese-language report; high user impact for non-DeepSeek providers.

10. **[#4906 — Show, don't tell: record a real session GIF](https://github.com/Hmbown/CodeWhale/issues/4906)** — README/site has no video/GIF of Codewhale running; fundamentally visual product described only in prose. Onboarding blocker.

## 4. Key PR Progress

1. **[#4992 — User command dispatch precedence & shadowing](https://github.com/Hmbown/CodeWhale/pull/4992)** — Layer 5.2 of the command-boundary refactor. Gherkin acceptance tests: user commands shadow built-ins, aliases, fallback semantics.

2. **[#4982 — Finalize Codewhale v0.9.2](https://github.com/Hmbown/CodeWhale/pull/4982)** — Release close-out: permission truth, Fleet setup/persistence, reasoning inspection, compaction errors, sub-agent supervision, sandbox truth, provider credential UX, ambient silhouettes.

3. **[#4979 — Detach foreground shell before steering](https://github.com/Hmbown/CodeWhale/pull/4979)** — Fixes #4930: blocking `sleep`/`cargo build` in foreground prevents user steering; moves wait to `/jobs` before enqueueing same-turn steer.

4. **[#4977 — AltGr-typed "/" reaches composer instead of help](https://github.com/Hmbown/CodeWhale/pull/4977)** — Fixes #4723: on Windows/ABNT2, AltGr+Q arrives as Ctrl+Alt+Q and matched global Ctrl-/ help chord. Also covers AZERTY.

5. **[#4990 — Devcontainer: support Windows development](https://github.com/Hmbown/CodeWhale/pull/4990)** — Dedicated dev image with Rust toolchain/rustfmt/DBus headers; named volumes instead of host HOME bind mount (invalid Windows HOME expansion).

6. **[#4981 — LaTeX environments/text/commands for math rendering](https://github.com/Hmbown/CodeWhale/pull/4981)** — Full environment-block support, inline commands, accents, case-insensitive matching, command-aware sub/superscripts.

7. **[#4984 / #4985 — Runtime config persistence + task workspace scoping](https://github.com/Hmbown/CodeWhale/pull/4984)** — GUI-facing TUI runtime API; `GET /v1/tasks` accepts optional `workspace` filter; TaskSummary includes workspace path.

8. **[#4980 — Publish and lock authorization order](https://github.com/Hmbown/CodeWhale/pull/4980)** — Closed: engine-level contract tests for tool admission, hooks, permission rules, auto-review, repository law, approval, sandbox enforcement.

9. **[#4942 — Preserve CRLF edits in edit_file](https://github.com/Hmbown/CodeWhale/pull/4942)** — LF-normalized search view maps spans back to original CRLF bytes; replacement newlines match base file style.

10. **[#4896 — Move terminal clipboard writes off event loop](https://github.com/Hmbown/CodeWhale/pull/4896)** — OSC 52 + SSH/tmux clipboard through one serialized background worker, bounded queue (1 request) to prevent unbounded backlog.

## 5. Feature Request Trends

- **Single-binary distribution**: Convergent demand across #3306, #4747, #3948 — ship one executable with library-backed TUI and in-process dispatch.
- **Desktop client**: #4986 requests a first-class desktop app (Codex Desktop-like) for users who don't want terminal/working-directory management.
- **Context diet & token attribution**: #4704–#4710 form a coordinated push to minimize every model-facing byte, deduplicate project/env/route/skill context, and add cross-model ablation gates.
- **CLI/TUI parity**: #4022 — subagent status, cancellation, and runtime controls must not be trapped in TUI; needed for future cloud/remote workflows.
- **Real usage documentation**: #4906 — session GIF/recording for README and site; product is visual but only described in prose.

## 6. Developer Pain Points

- **Compile times from the TUI crate monolith** (#4991): 14,878-line `main.rs`, 6,970-line subagent module, 771k Rust lines — developers report significant wait times during local iteration.
- **Config/secrets path fragmentation** (#2369): Windows/Cygwin home-directory divergence plus silent migration bugs; providers appear "missing" from fresh terminals (#4987).
- **Blocked foreground shell UX** (#4930): Enter during a blocking Bash command fails confusingly; fixes landing in #4979.
- **Provider compatibility errors** (#4978): Intermittent Anthropic-compatible API 400s ("type must be in enabled/disabled/auto") with no deterministic repro.
- **Perf regressions in skills discovery** (#3921): Full multi-root recursive rescan (depth 8, canonicalize per dir) on every prompt build, load_skill call, and /skills command.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*