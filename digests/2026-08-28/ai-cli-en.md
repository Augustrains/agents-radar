# AI CLI Tools Community Digest 2026-08-28

> Generated: 2026-08-28 07:19 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report — AI CLI Developer Tools
**2026-08-28**

---

## 1. Ecosystem Overview

The AI CLI tool landscape is in a phase of rapid iteration and platform consolidation. Release cadences remain high across the board, with OpenAI Codex shipping four alpha releases in 24 hours and Claude Code pushing two maintenance releases. A significant cross-cutting theme has emerged: **Windows desktop reliability** is the dominant pain point across multiple tools, with boot-loop failures, headless launches, and rendering regressions plaguing the latest distribution lines. Concurrently, communities are increasingly vocal about **model output quality**, **silent failure modes**, and the fragility of long-running sessions — issues that erode trust in autonomous agent workflows. There is also a visible push toward **enterprise readiness** (MCP discoverability, auth standardization, restricted/secure modes) alongside persistent demands for richer document handling and session lifecycle observability.

---

## 2. Activity Comparison

| Tool | Open Issues (24h) | PRs (24h) | Releases (24h) | Release Status |
|---|---|---|---|---|
| **Claude Code** | 10 (notable, incl. #77136 with 395 👍) | 1 (closed) | 2 (v2.1.248, v2.1.250) | Stable/active maintenance |
| **OpenAI Codex** | 10 (16 total, incl. #40700 with 36 comments) | 10 (9 closed, 1 open) | 4 (alphas 0.150–0.151) | Rapid alpha churn; Windows-heavy regressions |
| **Gemini CLI** | 10 (all P1–P3, 30 total active) | 10 (9 open, 1 closed) | 1 (nightly, no changes) | Nightly-only; maintainers heads-down on P1s |
| **GitHub Copilot CLI** | 10 (incl. #4612 13 GB log) | 0 | 2 (v1.0.81, v1.0.82-0) | GA features (MCP, plugins dashboard) |
| **Kimi Code CLI** | 4 (2 open, 2 closed) | 3 (2 open, 1 open since May) | 0 | Quiet; security bump pending |
| **OpenCode** | 10 (incl. #37012 with 43 👍) | 10 (9 PRs, 1 revert) | 2 (v1.18.24, v1.18.25) | Stable patches; Azure/Bedrock fixes |
| **Pi (pi-mono)** | 10 (community-flagged) | 10 (8 merged/closed, 2 open) | 0 | Active bug-fix cycle; no version bump |
| **Qwen Code** | 10 (incl. #5975 with 13 comments) | 10 (all open) | 1 (nightly) | Refactor-heavy; CI flakiness on main |
| **DeepSeek TUI** | 10 (incl. #5620) | 10 (8 closed, 2 open) | 0 | Release-consolidation phase (v0.9.12 pending) |

**Notable**: Codex has the highest PR velocity (10 PRs), Claude Code and OpenCode have the most stable release trains, Gemini and Qwen are in nightly-only or refactor-heavy phases.

---

## 3. Shared Feature Directions

These needs recur across multiple tool communities:

| Requirement | Tools Voicing It | Specific Needs |
|---|---|---|
| **Windows desktop reliability** | Claude Code, Codex, OpenCode, Pi | Backslash halving, headless launches, PSModulePath inheritance, `!`-command shell selection, PowerShell 5.1 vs 7 |
| **Session lifecycle hooks/events** | Claude Code, Copilot CLI, OpenCode, Qwen Code | Hooks on session start, resume, user-prompt transforms; fire on agent-initiated questions; content-level session search |
| **MCP config transparency & discoverability** | Claude Code, Copilot CLI, DeepSeek, Codex | Server registries, stale path fixes, phantom transport removal, local-executable support, config validation (settings.json schema) |
| **Provider compatibility & resilience** | Kimi, OpenCode, Qwen, Pi, Codex | Empty-`content` validation bugs, retryable network errors, `:free` model limits, whitespace-only tool results, SDK stagnation |
| **Stream/session integrity** | OpenCode, Pi, Gemini, Claude Code | Aborted turns bricking sessions, empty assistant messages causing 400/422s, lost background task errors, transcript corruption |
| **Tool/skill observability** | Codex, Gemini, Claude Code | Effective-tool listing in event streams, subagent context in bug reports, skill registry introspection |
| **Security hardening** | Claude Code, Gemini, Kimi, DeepSeek | Restricted modes, fail-closed workspace trust, dependency bump (asyncssh), env redaction before model context |

---

## 4. Differentiation Analysis

| Tool | Core Distinction | Target Users | Technical Approach |
|---|---|---|---|
| **Claude Code** | Deepest model-output-quality complaints; strongest enterprise push (restricted mode) | Professional developers, enterprise fleets, mobile/WFH workflows | `.md`-based skills, VSCode integration, transcript-based replay |
| **OpenAI Codex** | Fastest alpha cadence; Windows store/app distribution pain; strong alpha PR momentum | Heavy CLI users, desktop-app consumers, multi-model (ChatGPT/Classic) environments | Rust-based, app-server daemon, Guardian review layer |
| **Gemini CLI** | Structural refactor (OpenTUI migration); focus on agent-runtime correctness | TUI-first developers, local-model and sandbox users | Ink→OpenTUI, ACP unification, sandbox hardening |
| **GitHub Copilot CLI** | GA features (plugins dashboard, MCP 2026-07-28) with legacy UX conflicts | GitHub-centric developers, MCP-heavy power users | Hooks, settings.json config, background subagents |
| **Kimi Code CLI** | Enterprise-grade file-safety and security; deep MCP auth fixes | Security-conscious teams, JetBrains/ACP users | Python-based, asyncssh bump, UTF-8 validation |
| **OpenCode** | Strong Azure/Bedrock integration; billing transparency debates | Cloud-provider users, self-hosted, Windows users | Azure Auth via CLI, MCP SDK v2.0.0, stream-integrity series |
| **Pi (pi-mono)** | TUI polish and provider edge-case treadmill | TUI purists, local-first and OpenRouter users | Focused TUI fixes, proxy/NO_PROXY handling, configurable summarization |
| **Qwen Code** | Structural refactor (OpenTUI migration); active CI flakiness | Open-source contributors, enterprise self-host, Chinese-market users | OpenTUI batches, memory recall protocol, skill registry namespacing |
| **DeepSeek TUI** | Build-latency engineering; provider-neutrality audit | Terminal minimalists, multi-provider hosts, power users of TUI | Rust, gitoxide migration, dead-code sweep, performance folding |

---

## 5. Community Momentum & Maturity

- **Claude Code** has the broadest community energy (395 👍 on a single model-quality issue) and a maintained release train — but the community is deeply frustrated with model prose decline, not just tooling. Maturity: high, with enterprise features landing.
- **OpenAI Codex** is the most aggressive iterators (four alphas/week) but is burning community goodwill on Windows Desktop regressions (headless launches, boot loops, Send-button hangs). Maturity: high feature velocity, low perceived stability.
- **Gemini CLI** is technically ambitious (OpenTUI, sandbox hardening) but nightly-only cadence with P1 bugs unresolved suggests a stretched team. Maturity: mid, with a committed core community.
- **GitHub Copilot CLI** is consolidating GA features but has the quietest PR pipeline (0 PRs in 24h). Maturity: high, with enterprise trust.
- **OpenCode** is iterating steadily (v1.18.x patches) with clear recovery from Azure/Bedrock-specific issues. Community is vocal on billing/UI debates. Maturity: mid-high.
- **Pi, Qwen, DeepSeek** are all in refactor/consolidation phases — the innovation is real but the public velocity is lower. Pi's TUI polish cycle is notable; DeepSeek's 620-file monolith decomposition is a long-term bet.

---

## 6. Trend Signals

1. **Windows is the critical battleground for agentic CLI adoption.** Every major tool has a Windows-specific failure cluster this week. Tools that invest in first-class Windows testing (shell selection, path encoding, ConPTY/TUI interop) will win enterprise desktop workflows.

2. **Model output quality is a systems-level concern, not just a prompt-tuning issue.** Users are reporting "repetitive rhetorical tics" and prose incoherence across Claude versions, and API contract inconsistencies (Kimi's empty-`content` echo) are breaking clients. Tools need model-agnostic output validation and retryable error handling.

3. **Session integrity is the new reliability frontier.** Aborted turns bricking sessions, transcript corruption causing unrecoverable API errors, background tasks dying silently — these all erode trust in autonomous long-running agents. Expect "session recovery" to become a first-class feature.

4. **MCP is going mainstream, but configuration transparency is lagging.** Communities want registries, stale-path fixes, local-executable servers, and schema-validated configs. The tools that make MCP discoverable and debuggable will lead enterprise adoption.

5. **Security hardening is accelerating.** Restricted modes (Claude Code's `--restricted`), fail-closed workspace trust (Gemini), dependency bumps (Kimi's asyncssh), and secret-redaction-before-context (Gemini) signal that production deployment is the target — not just experimentation.

6. **Observability is becoming a differentiator.** Effective-tool listing in event streams (Codex), subagent trajectory sharing (Gemini), and session lifecycle hooks (Claude, Copilot, OpenCode) all indicate that power users want to *see what the agent is actually doing* — and why.

---

**Bottom line for decision-makers:** The AI CLI ecosystem is maturing rapidly but is still in a "pioneer tax" phase — the tools with the highest ambition (Codex, Gemini) are also carrying the highest instability cost. For production adoption, prioritize tools with stable release trains, Windows hardening, session-recovery mechanisms, and transparent MCP/configuration surfaces. For innovation velocity, watch Codex and OpenCode. The convergence of hooks, observability, and security hardening across all tools is a clear signal that the next 6–12 months will be about **making autonomous agents trustworthy at scale**, not just capable.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the provided data (as of 2026-08-28).

---

### 1. Top Skills Ranking

**Most-Discussed Skills (PRs) by Attention & Activity**

- **[skill-creator: Eval Harness Fixes (PR #1298)](https://github.com/anthropics/skills/pull/1298)** — **Status:** Open *(High Activity)*
  - **Functionality:** Fixes the core `run_eval.py` script that powers the skill-creator's optimization loop. The bug caused a 0% trigger rate, meaning the creator was optimizing descriptions against noise.
  - **Discussion Highlights:** This is the most critical pending fix. It is linked to 10+ independent reproductions of the bug (Issue #556). The discussion focuses on resolving the "claude -p" subprocess handling, Windows compatibility, and ensuring the eval artifact is properly installed as a real Skill.
- **[document-typography skill (PR #514)](https://github.com/anthropics/skills/pull/514)** — **Status:** Open
  - **Functionality:** Adds a quality-control Skill for AI-generated documents, specifically targeting "orphan words," "widow paragraphs," and numbering misalignment.
  - **Discussion Highlights:** The value proposition is high, as these typographic issues affect every document generated. The community discussion centers on the universality of the problem and the specificity of the proposed solutions for Claude to implement.
- **[scnet-hpc skill (PR #1615)](https://github.com/anthropics/skills/pull/1615)** — **Status:** Open *(Recent Activity)*
  - **Functionality:** A Skill for operating SCNet HPC clusters via SSH and Slurm workflows, covering job generation, cluster discovery, and profile management.
  - **Discussion Highlights:** Demonstrates a niche but strong demand for specialized infrastructure-as-code and HPC workflow automation directly within Claude Code.
- **[ODT skill (PR #486)](https://github.com/anthropics/skills/pull/486)** — **Status:** Open
  - **Functionality:** Enables Claude to create, fill, read, and convert OpenDocument (ODT) files and templates.
  - **Discussion Highlights:** Highlights the community's push for expanding document interoperability beyond the existing .docx/.pdf support to include ISO-standard open formats like LibreOffice.
- **[Hivemind: Multi-Agent Orchestration (PR #1628)](https://github.com/anthropics/skills/pull/1628)** — **Status:** Open *(Recent Activity)*
  - **Functionality:** A "zero-cost" orchestration Skill that delegates mechanical coding work to free/headless `opencode` workers, while Claude Code retains the roles of planner, reviewer, and merger.
  - **Discussion Highlights:** This is a highly innovative trend in the community: cost-optimization. The discussion centers on the architecture where the "expensive model's context is the scarce resource" and how to delegate sub-tasks to cheaper models.
- **[self-audit skill (PR #1367)](https://github.com/anthropics/skills/pull/1367)** — **Status:** Open
  - **Functionality:** A "quality gate" Skill that mechanically verifies output files exist before performing a four-dimension reasoning audit in priority order.
  - **Discussion Highlights:** addresses the growing need for reliability and verification in agentic workflows. The community is actively interested in "meta-skills" that audit AI output before delivery.

---

### 2. Community Demand Trends

From the Issues, the most anticipated new Skill directions are:

- **Security & Trust Boundaries:** The top issue (#492) concerns the security of the "anthropic/" namespace and preventing community-skill impersonation. This shows a strong demand for security-analysis skills and better trust verification.
- **Organizational Sharing & Management:** High demand (Issue #228) for organizational infrastructure—skills to share, manage, and synchronize Skills across teams. This points toward enterprise-level governance and collaboration features.
- **Developer Tooling Reliability:** The persistent issues surrounding `skill-creator` scripts (#556, #202) indicate the community wants the meta-tools for building skills to be production-grade and stable on all platforms (especially Windows), not just the skills themselves.
- **AI-Output Verification & Governance:** Multiple issues (#1385, #1329) propose "agent-governance," "self-audit," and "reasoning gates." There is a clear trend toward skills that act as safety/quality barriers, ensuring the agent doesn't ship unverified or incorrect work.
- **Context Window Efficiency:** Issue #1487 highlights that the `claude-api` skill injects ~156k tokens, exhausting context. There is a growing demand for "compact-memory" and state-management skills that minimize token usage.

---

### 3. High-Potential Pending Skills

These active PRs are likely to land soon and fill critical gaps:

- **[Windows & Subprocess Fixes for skill-creator (PR #1050 & PR #1099)](https://github.com/anthropics/skills/pull/1050)** — **Status:** Open
  - These PRs are second and third attempts to fix the Windows incompatibility (`.cmd` vs `.exe` and subprocess pipe reading) in the skill-creator scripts. They are crucial for unblocking Windows users from contributing and using the tooling effectively.
- **[testing-patterns skill (PR #723)](https://github.com/anthropics/skills/pull/723)** — **Status:** Open
  - A comprehensive skill covering testing philosophy (Testing Trophy model), unit testing patterns, and React component testing. This directly addresses a high-demand area: generating high-quality, idiomatic tests.
- **[ServiceNow platform skill (PR #568)](https://github.com/anthropics/skills/pull/568)** — **Status:** Open *(Long-running)*
  - A massive enterprise-oriented skill covering ITSM, ITOM, SecOps, and more for the ServiceNow platform. It is broad in scope and has been in discussion for months, indicating a large community effort addressing complex enterprise workflows.
- **[pyxel skill (PR #525)](https://github.com/anthropics/skills/pull/525)** — **Status:** Open
  - A skill for creating retro games with the Pyxel engine. It demonstrates a strong use case for creative coding, covering the "write → run → inspect → iterate" loop.

---

### 4. Skills Ecosystem Insight

The community's most concentrated demand at the Skills level is for **reliability and verification tooling**—not just for generating content, but for building meta-skills that ensure agent outputs are secure, token-efficient, and free of platform-specific bugs.

---

# Claude Code Community Digest — 2026-08-28

---

## 1. Today's Highlights

Two releases shipped in the last 24 hours: **v2.1.250** (bug fixes/reliability) and **v2.1.248** (introduces a `--restricted` mode that strips command-execution tools and ignores settings files — a meaningful step for sandboxed deployments). The community remains most agitated about **model output quality** — issue #77136 on repetitive rhetorical tics has 110 comments and 395 upvotes, making it the clearest signal that users want prose quality addressed as a first-class concern. A new batch of Windows and Remote Control reliability bugs also surfaced, with several tied to the latest release train.

---

## 2. Releases

### v2.1.250
- **Changes:** Bug fixes and reliability improvements only.
- **Takeaway:** Likely a patch for regressions introduced in 2.1.248.

### v2.1.248
- **New:** `--restricted` flag (or `CLAUDE_CODE_RESTRICTED=1`):
  - Removes built-in tools that run commands/code and `WebFetch` (unless explicitly in `--tools`)
  - Keeps file tools confined to the working directory
  - Refuses `bypassPermissions`
  - Ignores user, project, and local settings files
- **Takeaway:** This is a meaningful security boundary for CI/CD, untrusted repos, or managed fleets — expect follow-up issues as edge cases emerge.

---

## 3. Hot Issues

**1. [BUG] Model output quality deteriorating across model versions** — [#77136](https://github.com/anthropics/claude-code/issues/77136)
> *110 comments · 395 👍* — The community's loudest single issue. Claude 4.7/4.8/5.0/Fable reportedly default to repetitive rhetorical tics and struggle with coherent prose despite explicit style instructions. This is not a tooling bug — it's a model-behavior complaint that is severely affecting trust in output quality. Nearly 400 upvotes suggests wide impact across use cases.

**2. [BUG] Remote Control: auto-reconnect silently fails** — [#34255](https://github.com/anthropics/claude-code/issues/34255)
> *69 comments · 106 👍* — Connections drop with no recovery and no error. For teams relying on Remote Control for mobile or distributed workflows, this makes the feature effectively unreliable. Long-standing issue (since March) still open.

**3. [FEATURE] Microsoft Word (.docx) editing with track changes** — [#9631](https://github.com/anthropics/claude-code/issues/9631)
> *26 comments · 30 👍* — Users want to read/edit `.docx` files with track-changes support. The use case is evident: technical writing, contract review, and documentation workflows. No movement in ~10 months.

**4. [BUG] PDF support requires poppler-utils (undocumented)** — [#23704](https://github.com/anthropics/claude-code/issues/23704)
> *17 comments · 20 👍* — The Read tool claims PDF support but silently fails in containers without `poppler-utils`. No detection, no docs, no error message. A classic "it works on my machine" footgun.

**5. [BUG] Transcript JSONL records UI render metadata → unrecoverable API 400** — [#90002](https://github.com/anthropics/claude-code/issues/90002)
> *11 comments* — Newly reported (Aug 27). The Code tab writes `start_timestamp`/`stop_timestamp`/`flags` into the transcript, which then produces a permanent API 400 even after full sanitization. This breaks session replay and debugging workflows.

**6. [FEATURE] MCP Server Registry Discovery** — [#64633](https://github.com/anthropics/claude-code/issues/64633)
> *6 comments · 1 👍* — No built-in way to discover available MCP servers across an organization. Teams share URLs via wikis/Slack; each developer configures manually. A centralized catalog is the requested fix. Low engagement, but a structural gap for enterprise adoption.

**7. [BUG] Background Bash tasks killed mid-run silently** — [#84625](https://github.com/anthropics/claude-code/issues/84625)
> *4 comments* — `run_in_background: true` tasks die with no OOM, no user action, no error. Observed ~10 times in a week. Setsid-detached processes are immune. This is a critical reliability issue for long-running automation.

**8. [FEATURE] VS Code: "Search Sessions" should search content, not just titles** — [#77523](https://github.com/anthropics/claude-code/issues/77523)
> *3 comments · 2 👍* — Users need to re-find decisions from past sessions. Title-only search is insufficient. Simple, high-value UX improvement.

**9. [BUG] Windows/Git Bash: backslashes silently halved** — [#85856](https://github.com/anthropics/claude-code/issues/85856)
> *3 comments* — MSVCRT vs MSYS2 encoding mismatch halves backslashes in commands, and quoting cannot prevent it. Devastating for Windows users writing paths or regex in Bash tool calls.

**10. [BUG] Slash autocomplete broken after Windows Desktop update** — [#89628](https://github.com/anthropics/claude-code/issues/89628)
> *3 comments · 2 👍* — After the 2026-08-25 update: blank autocomplete, then first-position-only single-command behavior, chip styling gone. A clear regression in the desktop experience.

---

## 4. Key PR Progress

Only **1 PR** was updated in the last 24 hours — the repository is either in a quiet period or CI is backed up. For context, here is the active PR:

**Update frontend-design skill (v1.1.0)** — [#69226](https://github.com/anthropics/claude-code/pull/69226)
> *Closed.* Bumps the frontend-design skill plugin to 1.1.0 with "some improvements." No spec details; closed status suggests it was merged or rejected. Low-risk maintenance PR.

*Note: With only one PR in the window, this section is effectively a placeholder — the digest will be more informative when the PR pipeline is active.*

---

## 5. Feature Request Trends

| Direction | Signal | Representative Issues |
|---|---|---|
| **Enterprise MCP discoverability** | Centralized server registry/catalog; org-wide sharing | [#64633](https://github.com/anthropics/claude-code/issues/64633) |
| **Richer document support** | Word (.docx) editing with track changes; PDF without external deps | [#9631](https://github.com/anthropics/claude-code/issues/9631), [#23704](https://github.com/anthropics/claude-code/issues/23704) |
| **Voice / multimodal interaction** | Two-way voice for Cowork; image paste UX parity | [#90287](https://github.com/anthropics/claude-code/issues/90287), [#90286](https://github.com/anthropics/claude-code/issues/90286) |
| **Session search & recovery** | Content-level search; UI thread for held approvals | [#77523](https://github.com/anthropics/claude-code/issues/77523), [#85888](https://github.com/anthropics/claude-code/issues/85888) |
| **User-controlled UI** | Direct Browser pane access; incentives for data contribution | [#90284](https://github.com/anthropics/claude-code/issues/90284), [#90285](https://github.com/anthropics/claude-code/issues/90285) |
| **Security defaults** | Remote Control opt-in (not default-on); no bypasses | [#90179](https://github.com/anthropics/claude-code/issues/90179), [#90265](https://github.com/anthropics/claude-code/issues/90265) |

---

## 6. Developer Pain Points

- **Model output quality is the #1 frustration** — repetitive phrasing, incoherent prose despite explicit instructions, and a perceived decline across model versions (issue #77136). This dwarfs all other complaints in community energy (395 👍).

- **Windows remains a second-class citizen** — recurring, platform-specific breakage:
  - Backslash halving in Git Bash ([#85856](https://github.com/anthropics/claude-code/issues/85856))
  - Case-sensitive path comparison breaks worktree resume ([#85234](https://github.com/anthropics/claude-code/issues/85234))
  - Authenticode HashMismatch on shipped `claude.exe` ([#90283](https://github.com/anthropics/claude-code/issues/90283))
  - Slash autocomplete regression in Desktop ([#89628](https://github.com/anthropics/claude-code/issues/89628))

- **Silent failures erode trust** — background tasks killed without error ([#84625](https://github.com/anthropics/claude-code/issues/84625)), Remote Control dropping with no recovery ([#34255](https://github.com/anthropics/claude-code/issues/34255)), and transcript corruption producing unrecoverable API 400s ([#90002](https://github.com/anthropics/claude-code/issues/90002)). In each case, the user is left with no diagnostics.

- **Reliability of long-running sessions** — held-for-approval messages parked forever with no UI ([#85888](https://github.com/anthropics/claude-code/issues/85888)), daemon unreachable in CLI Agents View ([#80093](https://github.com/anthropics/claude-code/issues/80093)), Cowork VM teardown on idle with slow cold-boot recovery ([#81874](https://github.com/anthropics/claude-code/issues/81874)). Automation-heavy users are feeling the pain.

---

*Digest generated from GitHub activity between 2026-08-27 and 2026-08-28.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-28

## Today's Highlights

The Codex team shipped four new alpha releases (0.150.0-alpha.12.2 through 0.151.0-alpha.8) in the past 24 hours, continuing a rapid iteration cadence. Activity is dominated by Windows desktop stability issues — including a critical boot-loop bug where bundled codex.exe fails to relocate from WindowsApps (36 comments) and multiple reports of the desktop app launching headless with no renderer. On the PR side, the copyberry bot landed a substantial wave of merged work covering Guardian context rollover, history note image forwarding, and PowerShell sandbox compatibility fixes.

## Releases

Four alpha releases published in the last 24 hours:

- **rust-v0.150.0-alpha.12.2** — Patch release atop 0.150.0-alpha.12
- **rust-v0.151.0-alpha.6** — Sixth alpha of the 0.151 series
- **rust-v0.151.0-alpha.7** — Follow-up alpha, likely addressing issues found in .6
- **rust-v0.151.0-alpha.8** — Latest alpha in the 0.151 line

Release notes are minimal (`Release 0.151.0-alpha.8` style), suggesting these are incremental build-tag releases rather than feature announcements. The 0.151 line appears to be stabilizing after the 0.150 series, with the desktop app bundling 0.150.0-alpha.8 per issue reports.

## Hot Issues

1. **[#40700 — Codex Desktop cannot start: bundled codex.exe relocation from WindowsApps fails](https://github.com/openai/codex/issues/40700)** — 36 comments, Windows. The most active issue today. The Store-packaged Codex app fails to launch entirely because the bundled codex.exe cannot be relocated from the WindowsApps protected directory. This is a blocking issue for affected users — the app is completely unusable. High community engagement suggests a widespread Windows Store distribution problem.

2. **[#27117 — Windows standalone update inherits PSModulePath, breaking Get-FileHash](https://github.com/openai/codex/issues/27117)** — 23 comments, 18 👍. A long-lived issue (since June) that keeps attracting attention. When Codex (started from pwsh) launches a Windows PowerShell child process for updates, it inherits PowerShell 7 PSModulePath entries, causing `Get-FileHash` to fail. The 18 upvotes signal broad impact on Windows users.

3. **[#40860 — Invalid transport in mcp_servers.codex_app despite no config.toml entry (CLOSED)](https://github.com/openai/codex/issues/40860)** — 23 comments, 31 👍. Closed but heavily upvoted. The desktop app fails to resume threads because it injects an MCP transport config the user never created. The 31 upvotes make this one of the most-liked issues this week — users clearly want MCP configuration to be transparent and bug-free.

4. **[#41059 — Desktop remains headless after external CLI workaround](https://github.com/openai/codex/issues/41059)** — 14 comments. Windows app 26.820.9563.0. Even after users attempt CLI-based workarounds, the desktop UI never appears. Part of a worrying cluster of headless-launch reports on Windows this week.

5. **[#40342 — Paginated thread history projection stops at token_count record](https://github.com/openai/codex/issues/40342)** — 13 comments. On Linux. Thread history pagination breaks when it encounters a token_count record, preventing older history from loading. Affects both CLI 0.145.0 and 0.149.0, suggesting a long-standing bug in the history backend.

6. **[#26011 — config.toml MCP paths stale after auto-update](https://github.com/openai/codex/issues/26011)** — 11 comments, 7 👍. Windows. Auto-updates leave stale bin-directory paths in config.toml, breaking `node_repl` MCP startup (`os error 3`). Another Windows-specific update-pathology bug, consistent with the theme this week.

7. **[#40968 — Send button spins forever, prompts never submit](https://github.com/openai/codex/issues/40968)** — 11 comments. Windows 11. Follow-up prompts in Codex desktop never submit — the Send button spins indefinitely. Users on Pro subscription report this as a workflow blocker.

8. **[#31088 — Surface tool + skill catalog in --json event stream](https://github.com/openai/codex/issues/31088)** — 8 comments, 13 👍. CLI enhancement request. Developers want a first-class event describing the effective tools and skills offered to the model in `codex exec --json` and app-server events. Strong show of support for observability tooling.

9. **[#24704 — Forked subagents lose prompt-cache lineage](https://github.com/openai/codex/issues/24704)** — 5 comments, 17 👍. CLI. Subagents forked from a parent thread lose prompt-cache lineage despite inheriting a large prefix. Even though the issue is older (May), 17 upvotes signal this remains a meaningful cost/performance concern for heavy CLI users.

10. **[#41179 — ChatGPT Desktop launches headless after upgrade from Classic](https://github.com/openai/codex/issues/41179)** — 10 comments. Windows. A distinct headless-launch variant: upgrading from the "Classic" app to 26.820.9563.0 produces no renderer/window at all. Combined with #41059 and #38766, there is a clear Windows rendering regression cluster in the 26.820 line.

Also notable: [#41170](https://github.com/openai/codex/issues/41170) — first launch shows no window for ~15 minutes while extracting bundled cua_node runtime (performance issue), and [#41283](https://github.com/openai/codex/issues/41283) — npm install exits 0 leaving a broken CLI when platform tarball download fails (2 comments, created today), a dangerous silent-failure mode for installs.

## Key PR Progress

1. **[#41292 — Forward history note images to the model](https://github.com/openai/codex/pull/41292)** (open). Converts history backend images into `input_image` function-call output items, keeps image data out of logs and post-tool-use hooks. Important for multimodal history support.

2. **[#41260 — Let the history backend enforce tool output budgets](https://github.com/openai/codex/pull/41260)** (closed). Removes a duplicate client-side limit that could reject or truncate already-bounded backend responses. Cleanup that reduces spurious truncation errors.

3. **[#41243 — Add configurable gating for the sleep tool](https://github.com/openai/codex/pull/41243)** (closed). New `sleep_tool` feature flag independent of the clock tool, with `model_driven` and `always_on` modes. Gives developers finer control over agent tool exposure.

4. **[#41239 — Surface model provider auth recovery progress](https://github.com/openai/codex/pull/41239)** (closed). Emits turn-scoped `modelProvider/authRecoveryStarted` and `authRecoveryCompleted` app-server events. Improves observability for transient credential-refresh scenarios.

5. **[#41232 — Expose PowerShell version in environment context](https://github.com/openai/codex/pull/41232)** (closed). Adds `powershell_shell_version` feature flag; when enabled, includes the PowerShell major/minor version in `<environment_context>`. Directly relevant to the PSModulePath inheritance bug class (#27117).

6. **[#41227 — Use compatible PowerShell for elevated Windows sandbox commands](https://github.com/openai/codex/pull/41227)** (closed). Store PowerShell executables under `WindowsApps` can be inaccessible to the elevated sandbox account; this PR selects a compatible PowerShell instead. Likely mitigates a chunk of Windows sandbox issues.

7. **[#41221 — Honor turn token budgets in Guardian review rollover](https://github.com/openai/codex/pull/41221)** (closed). Preserves explicit token-budget preferences when deciding whether Guardian follow-up reviews need context rollover. Correctness fix for long-running Guarded sessions.

8. **[#41215 — Roll over Guardian context before follow-up reviews](https://github.com/openai/codex/pull/41215)** (closed). Long-lived Guardian sessions can exhaust the review model's context window; after rollover, a transcript delta is insufficient. This fix ensures persistent review instructions survive rollover.

9. **[#41223 — Add recency sorting to project/list](https://github.com/openai/codex/pull/41223)** (closed). Adds `recencyAt` derived from newest non-archived assigned thread; lets `project/list` sort by position or recency. UI/UX improvement for project-heavy workflows.

10. **[#41231 — Instrument the loaded plugin cache](https://github.com/openai/codex/pull/41231)** (closed). Adds hit/miss/wait/load metrics for the plugin cache and removes the unused force-reload path. Observability and cleanup work that should help debug plugin-related startup delays (cf. #41170).

Also worth watching: **[#10192 — Migrate TUI to app-server v2](https://github.com/openai/codex/pull/10192)** (open since January, updated today) — a long-running architectural PR that would unify the TUI and app-server protocols; **[#31471 — Extract apps cache into ConnectorRuntimeManager](https://github.com/openai/codex/pull/31471)** (open, faster-connectors series); and **[#15261 — Store guardian transcript boundary on review session](https://github.com/openai/codex/pull/15261)** (open, March).

## Feature Request Trends

- **Effective-tool observability (#31088)**: Developers want a first-class event describing exactly which tools and skills the model is offered, in both CLI JSON output and app-server streams. 13 👍 and counting.
- **Startup-page preference (#32673)**: Users want to choose whether the desktop app opens to "Work" or "Classic Chat" by default.
- **Goal-mode lifecycle improvements (#40162)**: Agents cannot reconfigure or resume a paused Goal after explicit user instruction — the tool creates an impossible lifecycle state (get_goal returns but cannot be altered). Users want resumable, reconfigurable goals.
- **Prompt-cache lineage preservation (#24704)**: Subagents should inherit parent prompt-cache prefixes to avoid paying full context costs on fork.
- **Configurable sleep/clock tool gating (#41243)**: The community is pushing for more granular feature flags to control which tools get registered, especially for long-running or background agents.

## Developer Pain Points

- **Windows desktop reliability is the dominant theme.** The WindowsApps relocation failure (#40700), two distinct headless-launch bugs (#41059, #41179), the 15-minute first-launch stall (#41170), and the Send-button hang (#40968) paint a picture of a Windows distribution in rough shape for the 26.820 line. This is compounded by auto-update pathology: stale config paths (#26011), PSModulePath inheritance breaking hashes (#27117), and proxy-related silent auth loss (#41136).
- **Update mechanics are fragile.** Three separate issues this week trace back to auto-update side effects (stale config paths, broken PowerShell child processes, headless post-upgrade launches). The auto-updater also force-kills active turns on app-server daemons after a 60s drain budget with no way to disable it (#40969).
- **Silent failure modes are particularly frustrating.** npm install exiting 0 while leaving a broken CLI (#41283) and Chrome native host going silently out-of-date (#40228) both fail without clear error signals.
- **Session/resume reliability is a cross-platform concern.** Thread-store ordinal failures (#40630), "already has an active writer" on resume (#39823), and empty voice placeholders that cannot be archived (#37058) all point to session-state management as a systemic weakness.
- **MCP configuration transparency.** Users want MCP server configuration to reflect reality — stale paths after update (#26011) and phantom transports (#40860) erode trust in the configuration system.

The rapid alpha cadence (four releases in 24h) suggests the team is actively burning down the Windows stability backlog, but the community is clearly feeling the pain of a release train moving faster than desktop QA can keep up.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-28

## Today's Highlights
Nightly build **v0.59.0-nightly.20260828** shipped with no user-facing changes. The maintainer team remains heads-down on a large backlog of agent-runtime bugs, with several P1 issues (subagent recovery misreporting, generalist agent hangs, shell command `Waiting input` stalls) still awaiting retesting. Community contributions this week focus heavily on hardening the sandbox environment and improving git configuration handling.

---

## Releases
- [v0.59.0-nightly.20260828.g3c311beac](https://github.com/google-gemini/gemini-cli/releases/tag/v0.59.0-nightly.20260828.g3c311beac) — Automated nightly version bump; no feature changes. [Full changelog](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260827.g3c311beac...v0.59.0-nightly.20260828.g3c311beac).

---

## Hot Issues
*(10 of 30 recently active; all open)*

1. **[#22323 — Subagent recovery after MAX_TURNS misreported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, 13 comments, 2 👍)  
   `codebase_investigator` reports `status: "success"` even when it hit the turn limit before doing any work. Misleading success signals erode trust in agent output — a critical correctness bug for multi-agent workflows.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, 8 comments, 8 👍)  
   Simple deferrals (even folder creation) hang for up to an hour. Community workaround: instruct the model never to defer to subagents. High community upvote count signals broad impact.

3. **[#25166 — Shell command stuck on "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, 4 comments, 3 👍)  
   Even trivial CLI commands hang after finishing, showing a phantom "awaiting input" state. Likely a state-machine bug in shell execution — frustrating for daily automation use.

4. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, 4 comments, 1 👍)  
   Browser agent exits with `Termination Reason: GOAL` despite failing. Linux/Wayland users are impacted; the error message is misleading and masks the root cause.

5. **[#21968 — Gemini underuses custom skills and subagents](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, 6 comments)  
   Anecdotal but repeated reports that the model ignores user-defined skills (gradle, git) unless explicitly instructed. For power users, this undermines the value of the entire skills system.

6. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, 5 comments)  
   Sessions deemed "low-signal" never get marked as processed, so they resurface repeatedly. Wastes background extraction budget on recycled content.

7. **[#26525 — Auto Memory: no deterministic redaction; excessive logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, 4 comments)  
   Secrets are sent to the model *before* redaction happens, and the service can log existing skill content. A security/privacy concern for teams running Auto Memory on local transcripts.

8. **[#24246 — 400 error with >128 tools enabled](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, 3 comments)  
   With many tools (MCP servers, skills, built-ins), the API rejects requests. Users expect the agent to scope tools to the task rather than exhausting the tool budget.

9. **[#22232 — Browser agent resilience: session takeover & lock recovery](https://github.com/google-gemini/gemini-cli/issues/22232)** (P3, 4 comments)  
   The browser agent uses fail-fast when a profile is locked (persistent sessions, orphaned processes). Users want automatic recovery instead of hard failures.

10. **[#20079 — Symlinked agent definition files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** (P2, 4 comments)  
    `~/.gemini/agents/foo.md` works, but a symlink to it doesn't. Breaks common dotfiles-management setups (e.g., chezmoi, yadm).

---

## Key PR Progress
*(10 of 25 recently active)*

1. **[#28930 — Drop unsafe `diff.external` override](https://github.com/google-gemini/gemini-cli/pull/28930)** (P1, core)  
   Fixes [#28928](https://github.com/google-gemini/gemini-cli/issues/28928): empty `diff.external` value isn't treated as "disabled" by git, causing sandboxed diffs to invoke external tools. Small fix, big correctness impact.

2. **[#28938 — Keep `GIT_CONFIG_*` triplets internally consistent](https://github.com/google-gemini/gemini-cli/pull/28938)** (P1, core)  
   Prevents Git from choking when redaction removes half of a numbered key/value pair in the environment. Also stops `ShellExecutionService` from restoring sensitive git config after sanitization.

3. **[#28939 — Avoid persisting interrupted-response placeholder](https://github.com/google-gemini/gemini-cli/pull/28939)** (P1, agent)  
   Fixes [#28927](https://github.com/google-gemini/gemini-cli/issues/28927): synthetic `[The previous response was interrupted…]` text gets replayed by the model, polluting session history. Subtle but important for long-running sessions.

4. **[#29110 — Route `read_file` through `FileSystemService`](https://github.com/google-gemini/gemini-cli/pull/29110)** (agent, core)  
   `read_file` bypasses the injected `FileSystemService`, while `write_file` and `replace` honor it. ACP-based clients advertising `fs: readTextFile` capabilities get inconsistent behavior.

5. **[#29099 — Fail-closed workspace trust; filter `mcpServers` in restricted mode](https://github.com/google-gemini/gemini-cli/pull/29099)** (security)  
   Prevents unintended process execution in `google-gemini-cli-a2a-server` when workspace trust fails. Filters repository-defined MCP servers in untrusted/restricted environments.

6. **[#29106 — Flush final SSE event on EOF](https://github.com/google-gemini/gemini-cli/pull/29106)** (core)  
   The SSE parser drops the final buffered event when a stream ends without a trailing blank line (truncated connections, non-conformant proxies). Loses `finishReason`/usage metadata silently.

7. **[#28863 — Extension consent: env changes + sanitize runtime vars](https://github.com/google-gemini/gemini-cli/pull/28863)** (extensions, security)  
   Extension updates could bypass user consent and inject unauthorized env vars into MCP server processes. Now folds MCP server env configs into consent strings and sanitizes custom variables.

8. **[#28942 — Strict boolean parsing for `DEBUG` env var in sandbox](https://github.com/google-gemini/gemini-cli/pull/28942)** (cli, platform)  
   Fixes [#28885](https://github.com/google-gemini/gemini-cli/issues/28885): `DEBUG=false` and `DEBUG=0` were treated as truthy due to JavaScript string truthiness. Three observable bugs traced to this.

9. **[#29104 — `[Skill]` tag in slash-command autocomplete & help](https://github.com/google-gemini/gemini-cli/pull/29104)** (agent, UX)  
   Mirrors the existing `[MCP]`/`[Agent]` visual treatment so users can distinguish user-installed skills from built-in commands in `/` menus.

10. **[#28926 — Windows longpaths setup docs in CONTRIBUTING.md](https://github.com/google-gemini/gemini-cli/pull/28926)** (docs, platform)  
    Addresses `~3,000 dirty staged files` caused by `core.longpaths` not being enabled on Windows. Practical fix for new contributors on Windows.

---

## Feature Request Trends
*(Distilled from all issue labels & descriptions)*

- **Auto Memory is a top focus** — Multiple P2s ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) reference retry loops, invalid patch quarantine, and redaction-before-context. The community expects the memory tier to be both *frugal* and *safe*.
- **AST-aware tooling is being investigated** — Two EPICs ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) explore read-once method extraction, precision search, and codebase mapping. Big potential win on token efficiency.
- **Persistent file-based task tracking** — Two issues ([#18836](https://github.com/google-gemini/gemini-cli/issues/18836), [#21000](https://github.com/google-gemini/gemini-cli/issues/21000)) push to replace in-context `WriteToDo` with file-backed CRUD. The community repeatedly calls out "context rot" and token costs of keeping todos in conversation history.
- **Subagent observability & trajectory sharing** — [#22598](https://github.com/google-gemini/gemini-cli/issues/22598) and [#21763](https://github.com/google-gemini/gemini-cli/issues/21763) ask for subagent context in `/bug` reports and shareable trajectories via `/chat share` — needed for evals and debugging.
- **Zero-dependency OS sandboxing** — [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) proposes a sandbox that leans into Gemini 3's native bash affinity (POSIX tools, chained `grep`/`sed`/`awk`) without heavy dependencies.

---

## Developer Pain Points

- **Agent hangs & phantom states** — Three separate P1s ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409), [#25166](https://github.com/google-gemini/gemini-cli/issues/25166), [#22465](https://github.com/google-gemini/gemini-cli/issues/22465)) describe hangs at interactive prompts, after command completion, and during generalist deferral. Developers can't trust long-running automation.
- **False success signaling** — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) and [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) both report `GOAL` termination despite actual failure. Misleading status is arguably worse than an explicit error because it silently corrupts downstream pipelines.
- **Skills/subagents aren't self-promoting** — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) and [#21432](https://github.com/google-gemini/gemini-cli/issues/21432) point to a recurring frustration: the CLI doesn't *know its own capabilities*, so power-user investments (custom skills, agents) sit idle unless manually invoked.
- **Environment hygiene is fragile** — Redaction gaps ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), environment triplet breakage ([#28938](https://github.com/google-gemini/gemini-cli/pull/28938)), and `DEBUG` truthiness bugs ([#28942](https://github.com/google-gemini/gemini-cli/pull/28942)) show that env handling is too brittle for enterprise use.

---

*Digest generated from public GitHub data on 2026-08-28.*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-28

## Today's Highlights

The Copilot CLI team shipped **v1.0.81** and **v1.0.82-0**, bringing the plugins dashboard to all users and rolling out full MCP 2026-07-28 protocol support across CLI, SDK, and IDE clients. Meanwhile, the community is wrestling with a fresh wave of regression reports — most notably a `store_memory` failure in 1.0.81 prereleases and a plugin-hook gap when resuming sessions. Several long-running stability issues (FileWatch event loops, event-storage exhaustion storms) continue to generate significant discussion.

## Releases

- **v1.0.82-0** — Patch release with general fixes and changes.
- **v1.0.81** (2026-08-27) — Notable updates:
  - **Plugins dashboard is now GA**: accessible via `/plugin`, `/mcp`, or `/skills`; opt out with `PLUGINS_DASHBOARD=false` (also disables `copilot plugins` command).
  - **MCP 2026-07-28 support** shipped to CLI, SDK, IDE, and in-memory clients.
  - **Hooks can now receive the current OpenTelemetry** context, enabling better tracing and observability integration.

## Hot Issues

1. **[#4535 — `store_memory` fails in v1.0.81 prereleases: "Instance id is required"](https://github.com/github/copilot-cli/issues/4535)**  
   The native memory writer is invoked without a required instance ID, breaking memory storage consistently. 7 comments in the last 24h signal active debugging. This is a core feature regression for a widely used capability.

2. **[#4612 — Runaway FileWatch host-event loop freezes TUI and grows debug log to 13 GB](https://github.com/github/copilot-cli/issues/4612)**  
   Long-running sessions can enter a tight loop emitting "No connection accepted a host event" — freezing the UI and generating massive log files. 6 comments; a serious reliability concern for unattended or overnight sessions.

3. **[#2873 — Copilot Pro subscription and Opus models](https://github.com/github/copilot-cli/issues/2873)**  
   Users report losing access to Opus models on Copilot Pro despite the request-multiplier model. Still open for 4+ months — a persistent concern for power users on Pro subscription tiers.

4. **[#3760 — "ctrl+enter enqueue" hint is wrong: ctrl+enter adds line break, ctrl+q enqueues](https://github.com/github/copilot-cli/issues/3760)**  
   The UI hint is incorrect on Windows, misleading users. 12 👍 reactions indicate broad agreement. Small UX bug, high visibility.

5. **[#4647 — v1.0.81 broke compatibility with chroma-mcp](https://github.com/github/copilot-cli/issues/4647)**  
   Fresh regression report (opened today): after upgrading from v1.0.80, the CLI no longer works with `chroma-core/chroma-mcp`. Likely related to the new MCP 2026-07-28 changes.

6. **[#4614 — macOS MallocStackLogging warning persists in v1.0.80](https://github.com/github/copilot-cli/issues/4614)**  
   The diagnostic "can't turn off malloc stack logging" still appears, despite prior fixes. 2 👍 reactions; noise-level concern for macOS users.

7. **[#4225 — Coordinator stuck "Working" while background subagent runs](https://github.com/github/copilot-cli/issues/4225)**  
   Queued input is neither answered nor shown as pending when a background subagent is active. Core orchestration UX issue still unresolved after several weeks.

8. **[#4602 — `store_memory` fails and all MCP servers stripped: managedSettings fails closed on serverFetchFailed flap](https://github.com/github/copilot-cli/issues/4602)**  
   A shared root-cause analysis: a managed-settings fetch failure cascades into memory-store failures and MCP server removal. Cross-cutting enterprise impact.

9. **[#4639 — Event-storage exhaustion retry storm drives Node OOM and GC/compaction loop](https://github.com/github/copilot-cli/issues/4639)**  
   Remote event-storage exhaustion leads to a flush-retry storm, memory pressure, and eventual OOM. Another long-running-session stability issue gaining traction.

10. **[#4486 — Edit permission request "times out" if not answered immediately](https://github.com/github/copilot-cli/issues/4486)**  
    Permission requests expire quickly, which is disruptive for users who keep multiple sessions open or leave sessions overnight. 1 👍, but the pain is real for multi-taskers.

## Key PR Progress

No pull requests were updated in the last 24 hours. Community PR activity is currently quiet, likely due to the recent release wave.

## Feature Request Trends

- **Smarter named sessions** — [#4642](https://github.com/github/copilot-cli/issues/4642): `--name` should create *or* resume a session, removing the need for users/automation to know which mode a session is in. Important for automation scripting and multi-session workflows.
- **Official settings.json JSON Schema** — [#4641](https://github.com/github/copilot-cli/issues/4641): Users want editor autocompletion and validation for the growing `~/.copilot/settings.json` file. Signals maturing configuration surface area.
- **Better `/diff` ergonomics** — [#4635](https://github.com/github/copilot-cli/issues/4635): Request to choose a custom base branch (e.g., `develop` vs. `main`) in `branch diff` view, not just current vs. local edits.
- **MCP local executable support** — [#4634](https://github.com/github/copilot-cli/issues/4634): Request for an MCP server "registry type" that resolves to a local executable rather than only npm/pypi/oci/docker.
- **Auditable rubber-duck reviews** — [#4621](https://github.com/github/copilot-cli/issues/4621): Users want verifiable records of model critique, findings, and resolution during rubber-duck reviews — addressing trust and repeatability concerns.

## Developer Pain Points

- **MCP protocol churn**: The 2026-07-28 MCP support is welcome, but it has already triggered at least one regression ([#4647](https://github.com/github/copilot-cli/issues/4647)). Users are asking for smoother protocol evolution and backwards compatibility.

- **Long-running session instability**: Multiple high-severity issues ([#4612](https://github.com/github/copilot-cli/issues/4612), [#4639](https://github.com/github/copilot-cli/issues/4639), [#4225](https://github.com/github/copilot-cli/issues/4225)) involve runaway loops, event-storage exhaustion, and UI freezes in sessions that run for extended periods. Reliability of long-lived sessions remains a top community concern.

- **Memory persistence flakiness**: [#4535](https://github.com/github/copilot-cli/issues/4535) and [#4602](https://github.com/github/copilot-cli/issues/4602) both surface failures in `store_memory` — either from missing instance IDs or from managed-settings fetch flaps. Memory features are fragile across configuration and network hiccups.

- **Hooks not firing consistently**: [#4629](https://github.com/github/copilot-cli/issues/4629) (hooks missing on `--resume`) and [#4640](https://github.com/github/copilot-cli/issues/4640) (`userPromptTransformed` skipped for steering messages) indicate the hooks system still has gaps around session lifecycle and edge-case message paths.

- **Model/compaction quirks on custom models**: [#4646](https://github.com/github/copilot-cli/issues/4646) (compaction failure with "Tool choice must be auto") and [#4645](https://github.com/github/copilot-cli/issues/4645) (`session.resume` ignores model override) frustrate users on custom-model setups — a growing segment as OpenRouter and similar gateways gain traction.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-28

## Today's Highlights
The community is actively surfacing two critical areas of concern: security hardening (via the asyncssh dependency bump) and data-integrity issues in file operations. A long-standing Notion MCP credential persistence bug has been closed after six months, while new reports highlight plan-mode agent looping and API round-trip validation problems that continue to frustrate developers.

## Releases
No new releases in the last 24 hours.

## Hot Issues

**#2623 — [bug] Plan mode: agent loops indefinitely on Bash echo / ReadFile instead of writing plan**  
*OPEN · created 2026-08-28 · 1 comment*  
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2623)  
Critical usability regression in v0.38.0 with the K3 model: after exploration completes, the agent fails to invoke `ExitPlanMode` and instead enters an infinite loop of redundant Bash echo/ReadFile calls. This effectively makes plan mode unusable in certain workflows. The single comment indicates this is reproducible in Linux environments.

**#2624 — docs: openai_legacy hosted /v1 example (not openai_responses, not /login)**  
*OPEN · created 2026-08-28 · 0 comments*  
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2624)  
Documentation gap for the `openai_legacy` provider type. Users are confused between `openai_legacy` (Chat Completions-compatible) and `openai_responses` wire protocols when configuring hosted /v1 endpoints. The issue outlines three specific configuration pitfalls that need explicit examples.

**#1211 — [bug] Notion Remote MCP creds are not stored beyond active session**  
*CLOSED · created 2026-02-23 · updated 2026-08-28 · 3 comments*  
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1211)  
After six months, this credential-persistence bug has been closed. Users running `kimi mcp auth` for Notion Remote were forced to re-authenticate on every session — a significant workflow disruption for Notion-backed agent workflows.

**#1272 — [enhancement] jetbrains-ai-assistant: using acp to call kimi cannot recognize the file**  
*CLOSED · created 2026-02-27 · updated 2026-08-28 · 1 comment*  
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1272)  
File attachment handling in JetBrains via ACP protocol is broken — Kimi cannot "see" attached files unless the user manually provides the full file path in the prompt. Now closed, suggesting an upstream fix has landed.

**#1279 — [enhancement] Feature Request: Native git-ai integration for AI code attribution**  
*CLOSED · created 2026-02-27 · updated 2026-08-28 · 0 comments*  
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1279)  
Request for native support of the vendor-agnostic git-ai standard, enabling `git blame` to distinguish AI-generated code from human edits. The lack of comments suggests this may have been closed as out-of-scope or already covered elsewhere.

**#2621 — 开发 Kimi API 都是吃 **** 的吗？ (Does everyone who develops Kimi API have to pay for ****?)**  
*OPEN · created 2026-08-27 · 0 comments · 👍 1*  
[View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2621)  
A frustrated bug report (in Chinese) about the API accepting its own responses with empty `content` but then rejecting them when echoed back with "text content is empty". The maintainers' own CLI apparently has this same workaround hardcoded — a strong signal of a systemic API contract inconsistency.

## Key PR Progress

**#2622 — deps: bump asyncssh to 2.23.1 in pykaos (GHSA-2wxc-x7rj-hg8f)**  
*OPEN · created 2026-08-28*  
[View PR](https://github.com/MoonshotAI/kimi-cli/pull/2622)  
Security-critical dependency update addressing two known vulnerabilities (GHSA-2wxc-x7rj-hg8f, GHSA-qr67-gv47-xwwh) in asyncssh 2.21.1. The pykaos workspace package is pinned to a vulnerable version — this bump is required for any security-conscious deployment.

**#2176 — fix(hooks): extract text from ContentPart for UserPromptSubmit hook**  
*OPEN · created 2026-05-07 · updated 2026-08-27*  
[View PR](https://github.com/MoonshotAI/kimi-cli/pull/2176)  
Fixes a silent failure where the `UserPromptSubmit` hook received an empty `prompt` and `matcher_value` whenever `user_input` was a `list[ContentPart]` (the default). This made regex matchers based on the prompt text completely non-functional. Addresses issue #2148.

**#2595 — fix(StrReplaceFile): refuse to edit files that are not valid UTF-8**  
*OPEN · created 2026-08-06 · updated 2026-08-27*  
[View PR](https://github.com/MoonshotAI/kimi-cli/pull/2595)  
Addresses a data-corruption bug (#2591): `StrReplaceFile` decodes with `errors="replace"`, so any non-UTF-8 byte in the file (even far from the edit target) becomes U+FFFD and is written back, irreversibly corrupting binary or non-UTF-8 text files. The fix refuses to edit such files outright.

## Feature Request Trends
- **AI Code Attribution**: The git-ai integration request (#1279) reflects growing demand for provenance tracking of AI-generated code — a trend consistent with broader industry pushes for AI code transparency.
- **IDE Ecosystem Integration**: The JetBrains ACP file-recognition bug (#1272) underscores the need for deeper, more reliable IDE integration, particularly around file/context handling in non-CLI environments.
- **Provider Configuration Clarity**: The documentation request (#2624) for `openai_legacy` indicates users are actively seeking interoperability with a wide range of OpenAI-compatible endpoints, suggesting a diversification of deployment targets beyond just Moonshot's hosted API.

## Developer Pain Points
- **Agent Loop Deadlocks**: Plan mode infinite-looping (#2623) is a recurring class of issue — the agent gets stuck in an exploration-evaluation cycle without converging on a plan artifact. This degrades trust in autonomous mode.
- **API Contract Inconsistency**: The empty-`content`-with-`tool_calls` validation bug (#2621) is a notable API-contract inconsistency — the API emits responses that it then rejects when echoed back. This forces clients (including the official CLI) to implement special-case workarounds.
- **Data Integrity Risks**: The StrReplaceFile UTF-8 corruption issue (#2591, per PR #2595) highlights a broader class of file-safety concerns. Developers expect LLM-driven file edits to be byte-safe; silent corruption of non-target bytes is a critical trust breaker.
- **Credential Persistence**: The Notion MCP auth issue (#1211) — while now closed — points to ongoing pain around session-scoped credentials in MCP integrations, a hurdle for production adoption of remote MCP tools.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-28

## Today's Highlights

Two quick patch releases (v1.18.24, v1.18.25) landed this week, fixing Bedrock caching bugs and finally enabling Azure CLI sign-in via Microsoft Entra ID—no more API key hunting. Meanwhile, the community is buzzing over an ongoing debate about the legacy UI layout (the most-thumbed issue this week), a suspected Go billing dashboard discrepancy, and a wave of session-integrity bugs where aborted or empty assistant messages brick conversations.

## Releases

**v1.18.25** — Azure authentication fixed: Azure CLI sign-in now works without requiring Bun.

**v1.18.24** — Bedrock reasoning responses no longer cached into unreplayable empty messages. Azure providers can now sign in with Microsoft Entra ID through the Azure CLI instead of requiring an API key. V1 now reads supported V2 config fields for forward compatibility.

## Hot Issues

1. **[#37012 — Keep legacy layout option (41 comments, 43 👍)](https://github.com/anomalyco/opencode/issues/37012)** — The most active community debate: users argue the classic UI offers faster access to everything from the main window and better workspace support. The new tabbed layout requires navigation to reach options. Clearly a passionate minority that wants the old UI preserved (or at least not deprecated).

2. **[#38255 — Discrepancy between OpenCode Go usage dashboards (9 comments)](https://github.com/anomalyco/opencode/issues/38255)** — A user's models stopped working, claiming 100% weekly usage, but the granular usage dashboard shows only ~$10 spent. Billing trust is critical — this needs a fix fast. Notably, a similar follow-up ([#45858](https://github.com/anomalyco/opencode/issues/45858)) reports percentage calculations that don't match actual usage ÷ quota math.

3. **[#44958 — Refusal response hidden; conversation history disappears (6 comments)](https://github.com/anomalyco/opencode/issues/44958)** — On OpenCode Go, a run can complete without any UI response, or hang indefinitely. HTTP stream completes successfully but the UI shows nothing. A silent failure like this is a top-priority bug.

4. **[#961 — Termux support (14 comments, 22 👍)](https://github.com/anomalyco/opencode/issues/961)** — Now closed, but a long-requested feature (since July 2025). Mobile/tablet developer workflows are a real demand; the community's persistence paid off.

5. **[#45087 — Auto-updater ate 266 GB in 10-minute loops (5 comments)](https://github.com/anomalyco/opencode/issues/45087)** — A long-running `opencode2 serve` process kept reinstalling beta packages every 10 minutes because the in-memory version never updates. A nasty disk-filling bug for any long-lived server deployments. Note the revert PR #45865 that pulls back an attempted fix.

6. **[#21658 — Azure AI Foundry Microsoft Entra OAuth (4 comments, 10 👍)](https://github.com/anomalyco/opencode/issues/21658)** — Corporate Azure users need Entra OAuth, not just API keys. This was just addressed in v1.18.24 for Azure providers, but the community wants it extended to Azure AI Foundry specifically.

7. **[#37946 — Aborted assistant turn bricks session (4 comments)](https://github.com/anomalyco/opencode/issues/37946)** — Aborting a frozen TUI turn persists an empty assistant message that gets replayed to providers as a 400 "must not be empty" error, permanently breaking the session. Related to a class of session-corruption issues, including [#31046](https://github.com/anomalyco/opencode/issues/31046) where empty text parts from tool-only responses cause 422s on strict providers.

8. **[#21034 — Gemma-4 model tool loops with OpenCode (21 comments, 20 👍)](https://github.com/anomalyco/opencode/issues/21034)** — Now closed. Gemma-4-26b/31b had persistent tool-call reliability issues even with latest tokenizer and engine patches. Many users want better support for self-hosted models, but this was non-trivial to solve.

9. **[#5409 — SessionStart hook for lifecycle events (7 comments, 18 👍)](https://github.com/anomalyco/opencode/issues/5409)** — Closed, but a genuinely useful feature request: hooks for session lifecycle events (SessionStart, etc.), similar to Claude Code. Not yet implemented judging by the issue state.

10. **[#17372 — Windows PowerShell 5.1 instead of PowerShell 7 (5 comments, 5 👍)](https://github.com/anomalyco/opencode/issues/17372)** — Closed, but a classic Windows developer pain point. OpenCode launched from pwsh still uses legacy PowerShell 5.1 for bash commands, meaning profiles and env vars don't carry over. It's a polarizing platform issue that affects all Windows users with custom setups.

## Key PR Progress

1. **[#45777 — Upgrade MCP SDK to modern protocol (v2.0.0)](https://github.com/anomalyco/opencode/pull/45777)** — Replaces `@modelcontextprotocol/sdk@1.29.0` with the split client/core/server 2.0.0 packages. Negotiates MCP 2026-07-28 on HTTP/stdio while maintaining backward compatibility with legacy servers. A significant infrastructure modernization.

2. **[#40125 — Per-MCP-server trust configuration](https://github.com/anomalyco/opencode/pull/40125)** — Instead of a global insecure toggle, this adds fingerprint pinning to trust specific self-signed certs and `caFile` for private CAs. Addresses a real security/complexity tradeoff for enterprises.

3. **[#45864 — Keep chat reasoning in one lifecycle](https://github.com/anomalyco/opencode/pull/45864)** — Fixes #45791 where `openai-chat` eagerly ended reasoning blocks when visible content arrived, causing empty `reasoning-0` blocks to be re-opened. Part of a series of AI-stream integrity fixes.

4. **[#45861 — Continue retryable failures after durable output](https://github.com/anomalyco/opencode/pull/45861)** — Previously, if a retryable failure hit after the assistant produced output, the session was stuck. Now recovery continues if the provider streams partial output before failing. Critical resilience fix for long-running sessions.

5. **[#45854 — Respect response text and reasoning finals](https://github.com/anomalyco/opencode/pull/45854)** — Providers that send a corrected final value after streaming deltas previously had the draft saved. Now the final value is cached and used at the fragment boundary. Part of the "stream integrity" theme.

6. **[#45842 — Skip Bedrock cache point below minimum cacheable size](https://github.com/anomalyco/opencode/pull/45842)** — Bedrock rejects cache points when the cached prefix is too small. This fixes the failure by detecting the model's minimum threshold and skipping `applyCaching()`. Small but prevents provider errors.

7. **[#44966 — Terminal event exit completion handling](https://github.com/anomalyco/opencode/pull/44966)** — Fixes the CLI not exiting after the primary session emits a terminal `step_finish` event with reason `exit`. If you've ever had a lingering CLI process, this is the fix.

8. **[#45182 — Restore SSE payload schemas in OpenAPI](https://github.com/anomalyco/opencode/pull/45182)** — The generated OpenAPI doc currently treats SSE data as opaque strings, making `V2Event` and `SessionLogItem` unreachable for API consumers. Fixes #44911 for correct schema generation.

9. **[#45852 — Autonomous auto-drive execution engine (draft)](https://github.com/anomalyco/opencode/pull/45852)** — A bold proposal to shift from "prompt-and-halt" to autonomous cruising; the engine tracks the original goal and context across turns to self-drive the session toward completion. Ambitious and potentially paradigm-shifting, still early.

10. **[#45865 — Revert auto-update fix](https://github.com/anomalyco/opencode/pull/45865)** — Reverts #45091, the original fix for the 266 GB auto-updater bug. This suggests the first patch caused regressions; the team is taking a step back to find a cleaner solution.

## Feature Request Trends

- **UI layout flexibility**: The #37012/#37527 debate over the legacy layout is the strongest signal — power users want denser, single-window access without sacrificing new features. Expect more "stability mode" and workspace-related asks.
- **Billing and usage transparency**: Multiple issues (Go dashboards, referral rewards, billing history) indicate a strong desire for a self-serve billing portal with clear usage breakdowns and refunds.
- **Authentication standardization**: Azure Entra OAuth for all Azure surfaces, not just the base provider. Corporate users want passwordless, keyless auth.
- **Session lifecycle hooks**: `SessionStart` and similar event hooks keep recurring — the community wants plugin-driven lifecycle automation.
- **Document/offline preview**: PRs #45853/#45857 add offline previews for docx/xlsx/pptx/pdf directly in the app, a productivity-oriented feature likely to land soon.

## Developer Pain Points

- **Session bricking from empty assistant messages**: Multiple issues ([#37946](https://github.com/anomalyco/opencode/issues/37946), [#31046](https://github.com/anomalyco/opencode/issues/31046)) show that aborted or tool-only responses leave persisted empty `TextPart`s that trigger provider 400/422 errors on the next turn. This is the nastiest class of bug right now — it destroys session state permanently.
- **Auto-updater and long-running process quirks**: The 266 GB disk-fill bug highlights that the update loop in long-lived processes is fragile; a revert means the fix is still in flux.
- **MCP reliability**: Remote MCP clients lacking transport-level retries, plus truncation issues with large data, are recurring complaints. The SDK upgrade to v2.0.0 in #45777 may address some of this, but users want more resilience.
- **Windows-specific issues**: PowerShell 5.1 vs 7, `.exe` suffix leaking into process names, and node-pty AttachConsole errors — Windows remains a second-class citizen, and the community is vocal about it.
- **Billing-account handling**: Accidentally applying rewards to the wrong account ([#45803](https://github.com/anomalyco/opencode/issues/45803)) and a lack of billing history ([#34376](https://github.com/anomalyco/opencode/issues/34376)) show real friction around the Go subscription model — users want more control and transparency over their spend.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-28

## Today's Highlights
The last 24 hours saw a burst of TUI-related fixes landing, addressing long-standing rendering and terminal-interop pain points. Notably, a cluster of issues around text wrapping corruption (word-per-line rendering) and soft line-break handling received both well-received patches and new reproductions. On the provider-compat front, fixes landed for DeepSeek-family reasoning replay, proxy-agent regressions, and OpenRouter `:free` model failures.

## Releases
No new versions were published in the last 24 hours.

## Hot Issues
1. **[#8584 — TUI row corruption during streaming](https://github.com/earendil-works/pi/issues/8584)** — Assistant text renders one word per line after tool calls with long output lines. This is the most active open issue (14 comments, 6 👍). The root cause appears to be state corruption in the TUI's scroll/offscreen handling rather than markdown parsing, making it distinct from the soft-break issue below. Community urgency is high because it makes long agent runs effectively unreadable.

2. **[#6922 — Default model cannot be a llama.cpp model](https://github.com/earendil-works/pi/issues/6922)** — Closed but still one of the most-upvoted issues of the month (14 👍). When users set `defaultProvider` to `"llama.cpp"`, pi refuses to start ("No models available"). The closure suggests a workaround exists, but the high vote count indicates significant demand for local-first configurations.

3. **[#7553 — Configurable thinking level/model for compaction](https://github.com/earendil-works/pi/issues/7553)** — In-progress feature request (9 comments) to decouple compaction's thinking budget from the session's. Auto-compaction on reasoning models is currently burning the same reasoning budget as normal turns, making summarization expensive and slow. PR #7602 aims to close this.

4. **[#8675 — TUI word-per-line wrapping (0.84.3, WSL2)](https://github.com/earendil-works/pi/issues/8675)** — Duplicate of #8621 with a consistent repro in WSL2/Windows Terminal. The existence of multiple reports (and auto-closed duplicates) suggests this is a Windows/ConPTY-specific interaction with the TUI's width detection. 4 👍 indicate meaningful user impact.

5. **[#8762 — Session list fully parses every session file](https://github.com/earendil-works/pi/issues/8762)** — Performance bug: the `--resume` selector parses entire JSONL files (allMessagesText, messageCount) even though the picker only shows names. Slow to open for power users with large session stores; the fix is likely a lazy/streaming read of just the header.

6. **[#8757 — Tool-arg validator doesn't coerce object/array for string params](https://github.com/earendil-works/pi/issues/8757)** — The validation layer repairs JSON strings to structured types, but the mirror direction (object/array → string) is missing. This breaks `write`/`edit` content when models send structured payloads instead of plain strings, causing "must be string" errors mid-task.

7. **[#8752 — bedrock-converse usage.input not normalized](https://github.com/earendil-works/pi/issues/8752)** — Anthropic models on Bedrock report input net of cache; OpenAI-family report it gross. Copies `inputTokens` straight through, causing false cache-miss notices and doubled input cost calculations. Hard to detect for most users but financially significant for heavy Bedrock users.

8. **[#8760 — OpenRouter `:free` models fail with 400](https://github.com/earendil-works/pi/issues/8760)** — Pi sends `max_tokens` equal to the catalog's `maxOutputTokens`, which exceeds upstream `:free` provider limits. This blocks an entire model class from working. Recently filed but affects many `:free` models, so the fix may be simple clamp logic.

9. **[#8711 — TUI pegs 100% CPU on OpenRouter GLM-5.3-flash](https://github.com/earendil-works/pi/issues/8711)** — Processing a small openrouter connection (`thinking` mode) leads to pathological CPU use and TUI freeze. Root cause identified in issue body: `reasoning_details` stored as one object per token during streaming, creating a huge transcript that is re-rendered/parsed each time.

10. **[#8763 — Windows: `!`-prefixed config shell commands fail](https://github.com/earendil-works/pi/issues/8763)** — API keys/headers resolved via `!command` ignore `settings.shellPath` and pick up the WSL bash shim. Auth silently fails for Windows users with custom shell configs. Fixed in PR #8764 (see below).

## Key PR Progress
1. **[#8674 — fix(tui): render markdown soft line breaks as spaces](https://github.com/earendil-works/pi/pull/8674)** — Fixes #8673 by mapping CommonMark soft breaks to spaces instead of hard breaks in the TUI renderer. Makes thinking blocks flow as paragraphs instead of ragged lines. Small, targeted, and the right semantic fix.

2. **[#8732 — fix(ai): preserve reasoning_content on cross-model replay](https://github.com/earendil-works/pi/pull/8732)** — Fixes #8728. When replaying history into a DeepSeek-family endpoint, assistant messages that carried reasoning content must re-include it, otherwise the endpoint rejects the request with 400. Applies to DeepSeek-compatible gateways, not just the official API.

3. **[#8723 — fix(coding-agent): expose https-proxy-agent named export](https://github.com/earendil-works/pi/pull/8723)** — Addresses the v0.84.3 regression where code splitting broke `HttpsProxyAgent` (issue #8610). The fix adds a custom build plugin to emit a proper named export chunk. This is load-bearing: proxy users on google-vertex were fully blocked.

4. **[#8737 — fix(ai): match subdomains and root domains in NO_PROXY](https://github.com/earendil-works/pi/pull/8737)** — Improves NO_PROXY parsing for wildcard domains (`*.example.com`) and bare domains, plus proper IPv6 handling. A large class of proxy misconfigurations disappear once this lands.

5. **[#8764 — fix(coding-agent): honor settings.shellPath for `!` command resolution](https://github.com/earendil-works/pi/pull/8764)** — Fixes #8763. `getShellConfig()` only honored the explicit arg, so config/header shell commands ignored `settings.shellPath` and fell back to the WSL shim on Windows. A one-line caller fix with broad impact for Windows users.

6. **[#7602 — feat(coding-agent): configurable summarization models](https://github.com/earendil-works/pi/pull/7602)** — Open PR closing #7553. Adds configurable models and thinking levels for compaction and branch summaries, including provider-error handling for context-window limits. This unlocks cheaper/faster compaction for reasoning-model users.

7. **[#8719 — fix(ai): treat whitespace-only tool results as empty output](https://github.com/earendil-works/pi/pull/8719)** — Filters out whitespace-only tool results (e.g. `"\r\n"` from Windows shells) before sending to OpenAI-compatible providers that reject empty `tool` message content with 400.

8. **[#8727 — fix(tui): preserve scrollback on offscreen changes](https://github.com/earendil-works/pi/pull/8727)** — Keeps historical scrollback as native snapshots instead of clearing/replaying the full transcript when the viewport is not visible. Aims to fix the visible "scrollback panic" behavior in long-running sessions.

9. **[#8731 — feat(tui): allow disable copy on fullscreen, ctrl + x copies selection](https://github.com/earendil-works/pi/pull/8731)** — Implements the long-requested setting (issue #7720) to disable copy-on-select in fullscreen TUI, plus Ctrl+X hotkey for explicit copy. Merged after a 3-week wait; the community solution landed quickly once addressed.

10. **[#8766 — feat(coding-agent): make write and edit output easier to scan](https://github.com/earendil-works/pi/pull/8766)** — New open PR to give `Write(path)` and edit previews a compact file-focused presentation with line numbers and diffs. Targets the most-reviewed output surface — where users spend time verifying changes.

## Feature Request Trends
- **TUI polish**: Multiple requests for configurable copy behavior (disable on select), granular mouse selection (single columns in tables), and more readable markdown (soft-brake mapping, thinking block formatting) — all actively being addressed.
- **Local configuration & model control**: Requests to make llama.cpp the default provider, configurable compaction models/thinking levels, and global `~/.agents/AGENTS.md` confirm a shift toward local-first and per-session-model control.
- **Settings ergonomics**: JSONC support for settings files (comments/trailing commas) and an installation section in the README show concern with approachability of the tool and its config format.
- **Extension API growth**: Exposing the TUI's `openUrl` handler to extensions (via ExtensionAPI) signals developers want to hook into the fullscreen TUI surface for custom tooling.
- **Recent feature additions**: Configurable `copyOnSelect` (PR #8731), UI prompt events (PR #8355) for extensions to indicate "Waiting for user input" states, and opt-in overlay selection exclusion (PR #8744) suggesting the TUI extensibility surface is growing steadily.

## Developer Pain Points
- **TUI wrapping/rendering regressions**: The recurrence of word-per-line wrapping and scrollback clearing dominates issue triage; the codebase appears fragile around streaming large tool outputs and holding viewport state. Multiple duplicates and auto-closes indicate the maintainers are keeping the issue tracker clean but community frustration is real.
- **Provider compatibility is a treadmill**: The proxy-agent regression from the latest version, whitespace-only tool-result 400 errors, Bedrock input normalization gaps, and `:free` model `max_tokens` mismatches all trace to differences between OpenAI-compatible surface areas. Each week brings 2-3 new edge cases that block a subset of users from working entirely.
- **Windows and WSL2 are second-class**: Between the `!`-command resolution and the WSL2 rendering issues, Windows configurations continue to be underserved. The fixes are small when they land, but the frequency of Windows-specific bugs is noticeable.
- **Performance at scale**: Issues #8762 (slow session list) and #8711 (100% CPU with reasoning tokens) point to quadratic parsing/re-rendering behavior as session sizes grow — a theme that will become more pressing as models produce longer reasoning traces.

---
*Sources: `github.com/badlogic/pi-mono` and linked issues/PRs.*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-28

## Today's Highlights

The project shipped a nightly release (v0.22.2-nightly.20260828) with fixes for web-shell session diffs and DingTalk rich-text channels. Notable momentum continues on major refactors: the OpenTUI migration is now in its third implementation batch (PR #10368), and a new standalone voice daemon package `qwen-live` has been proposed (PR #10367). On the bug front, a recurring pattern of E2E CI failures on main generated multiple auto-tracked issues, prompting several test-isolation and fixture-reuse fixes.

---

## Releases

**v0.22.2-nightly.20260828.7357136dd1** ([release](https://github.com/QwenLM/qwen-code/releases/tag/v0.22.2-nightly.20260828.7357136dd1))

- `fix(web-shell)`: restore saved session diffs ([PR #10093](https://github.com/QwenLM/qwen-code/pull/10093))
- `fix(channels)`: preserve DingTalk rich-text multi-… (incomplete in data)

---

## Hot Issues

1. **[#5975 — API Error: No stream activity for 120000ms after 19 chunks](https://github.com/QwenLM/qwen-code/issues/5975)** (P2, open, 13 comments)
   The most-commented open issue. Since v0.19.3, users experience stream timeouts after thinking output; awaiting triage. Community visibly frustrated — 13 comments without a fix landed.

2. **[#8662 — Migrate TUI rendering layer from ink to OpenTUI](https://github.com/QwenLM/qwen-code/issues/8662)** (P3, tracking, 11 comments)
   A structural refactor canvassing ink 7 + React 19 with a 1,037-line patch and custom VP mode. Flicker and rendering inconsistencies are the driving pain; this is the umbrella issue for PR #10368.

3. **[#4063 — core + cli architecture review: 12 structural issues](https://github.com/QwenLM/qwen-code/issues/4063)** (in-progress, 11 comments)
   Highlights tight coupling to `@google/genai` types across 136 files, among other P0 architecture concerns. A long-running community-driven audit that continues to gather feedback.

4. **[#10227 — Custom model provider cannot chat](https://github.com/QwenLM/qwen-code/issues/10227)** (P2, need-info, 7 comments)
   Moonshot-flavored JSON schema validation error (`properties must be an object`). Echoes a broader class of provider-compatibility complaints.

5. **[#8083 — Make derived Config context ownership explicit](https://github.com/QwenLM/qwen-code/issues/8083)** (P1, closed, 7 comments)
   Proposed replacing ad hoc `Object.create(base)` overrides with explicit ownership in derived `Config` instances — the issue is now closed, presumably resolved.

6. **[#9005 — Anthropic wire lacks stream-safety protections](https://github.com/QwenLM/qwen-code/issues/9005)** (P1, in-progress, 6 comments)
   `anthropicContentGenerator` misses protections the OpenAI wire already has; `@anthropic-ai/sdk` pinned to Jan 2025 `^0.36.1`. A clear parity gap with provider-specific SDK stagnation.

7. **[#10065 — LM Studio grammar parse failure](https://github.com/QwenLM/qwen-code/issues/10065)** (P2, ready-for-human, 6 comments)
   Local LM Studio (0.4.21) fails with "failed to parse grammar" even with MCP servers disabled and `tools.core=[]`. Impacts the local-model developer segment.

8. **[#9475 — Assistant reasoning messes up mid-screen](https://github.com/QwenLM/qwen-code/issues/9475)** (P2, UI, 4 comments)
   Reasoning updates randomly reflow text in the middle of the screen; tool-call output sticks to the bottom until final response. Core interactive rendering bug, `welcome-pr`.

9. **[#10356 — Main CI failed: E2E Tests on 148273956b5c](https://github.com/QwenLM/qwen-code/issues/10356)** (ready-for-agent, 4 comments)
   Part of a surge of auto-tracked main branch E2E failures. Signal of flaky tests, not necessarily product regressions; PR #10340 targets the underlying tool-control flake.

10. **[#10348 — Hooks: support agent-initiated question triggers](https://github.com/QwenLM/qwen-code/issues/10348)** (P3, closed, 4 comments)
    Request to fire hooks when an agent raises a question — especially under yolo mode — to enable Feishu or desktop push notifications. Closed, likely as a duplicate or out of scope.

---

## Key PR Progress

1. **[#10368 — feat(cli): OpenTUI migration live-session and input batch](https://github.com/QwenLM/qwen-code/pull/10368)** (open)
   Third batch of the OpenTUI migration: live-session stream fold, message rendering with streaming markdown heal, progressive MCP displays. Answers issue #8662.

2. **[#10367 — feat(qwen-live): standalone voice daemon package — M1 + M2](https://github.com/QwenLM/qwen-code/pull/10367)** (open)
   New incubating package implementing minimal voice loop and rich interaction, keeping `packages/cli` untouched. Part of the Live split roadmap (#10118).

3. **[#10347 — fix(core): auto-retry transient network errors (EOF) where Ctrl+Y is unavailable](https://github.com/QwenLM/qwen-code/pull/10347)** (open)
   Re-classifies 4xx status codes that wrap low-level network failures (e.g., `400 network error ... EOF`) as retryable transport errors — extending bounded auto-retry to channels without interactive Ctrl+Y.

4. **[#9940 — fix(review): reply carried findings into their thread, resolve fixed ones](https://github.com/QwenLM/qwen-code/pull/9940)** (open, autofix/takeover)
   Multi-round review findings now reply inside their original thread rather than spawning inline comments; fixed findings are fed back to the PR for resolution.

5. **[#10319 — fix(cua): harden Computer Use sessions and instructions](https://github.com/QwenLM/qwen-code/pull/10319)** (open)
   Real `AbortSignal` with 25s deadline, typed timeouts, authorization expiry handling for Node REPL Computer Use.

6. **[#10268 — fix(daemon): Cancel timed-out session initialization](https://github.com/QwenLM/qwen-code/pull/10268)** (open, review/self-reported)
   Makes session initialization budget authoritative end-to-end: private absolute deadline propagated through config, Gemini startup, and `SessionStart` hooks.

7. **[#10183 — feat(memory): add structured on-demand recall](https://github.com/QwenLM/qwen-code/pull/10183)** (open)
   Shifts auto-memory from a flat body-heavy prompt to a structured push/pull protocol: two-level ref/title tree, query-focused metadata subtrees, and a dedicated recall tool.

8. **[#10049 — feat(skills): namespace extension skill registry keys by extension name](https://github.com/QwenLM/qwen-code/pull/10049)** (open)
   Extension skills get `<extension>:<name>` keys, unifying Skill tool lookup, `<available_skills>` context, slash-command registration, and `skills.disabled` matching.

9. **[#9769 — feat(web-shell): unblock git update on dirty working tree](https://github.com/QwenLM/qwen-code/pull/9769)** (open)
   Replaces dead-end error with a resolution panel offering two ways forward when `pull` is blocked by uncommitted changes.

10. **[#9970 — perf(cli): reduce TUI render overhead](https://github.com/QwenLM/qwen-code/pull/9970)** (open)
    Incremental terminal output in virtual-viewport mode plus memoized history body; legacy rendering unchanged.

---

## Feature Request Trends

- **TUI/rendering overhaul (OpenTUI)**: The ink-based renderer is a recurring pain point (flicker, mid-screen text jumps, rendering overhead). The migration is now actively landing in batches.
- **Event/hook enrichment**: Multiple requests for hooks that fire on agent-initiated events (e.g., questions under yolo mode), targeting external push notifications (Feishu, desktop).
- **Structured memory & recall**: PR #10183 signals a move toward structured, on-demand memory recall rather than flat prompt stuffing.
- **ACP (Agent Client Protocol) unification**: Issue #10061 pushes for one transport-agnostic ACP core (stdio + HTTP) and an SDK bump to 1.x.
- **Provider resilience**: Auto-retry for transient network errors (EOF) in non-interactive channels — a direct response to user-facing timeouts in chat integrations.
- **Voice/live interactions**: New `qwen-live` package explores standalone voice daemon capabilities.

---

## Developer Pain Points

1. **Stream timeouts and retry friction** — Issue #5975 is the top-voted pain: thinking output followed by no stream, leading to `No stream activity for 120000ms` errors. Compounded by Ctrl+Y-only manual retry in some channels (**#10347** directly addresses this).

2. **E2E CI flakiness on main** — A wave of auto-generated issues (`#10356`, `#10350`, `#10313`, `#10311`, `#10281`, etc.) from main-branch E2E failures suggests test instability is eroding developer confidence — PRs #10340 and #10365 are targeted fixes.

3. **Provider incompatibilities** — Custom providers (Moonshot, LM Studio, DeepSeek) intermittently fail on schema validation, grammar parsing, or reasoning-content mismatch. Suggesting a wider request-root validation gap at the provider-adapter layer.

4. **Architecture coupling and technical debt** — The `@google/genai`-type coupling across 136 files (**#4063**), the 1,000+ line ink patch (**#8662**), and fused slash-command/UI contracts (**#9150**) are recurring structural frustrations.

5. **Dirty workspace / session lifecycle issues** — Dead-ends on dirty working trees (**#9769**) and leftover project snapshots from temp dirs (**#9110**) indicate edge cases in workspace lifecycle management still need attention.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest
**2026-08-28** | Source: [github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI)

---

## 1. Today's Highlights

The v0.9.12 release cycle is consolidating rapidly — the integration branch ([#5576](https://github.com/Hmbown/CodeWhale/issues/5576)) has closed on release-blocker items, folding in two performance PRs ([#5664](https://github.com/Hmbown/CodeWhale/issues/5664), [#5665](https://github.com/Hmbown/CodeWhale/issues/5665)) and a test-only helper cleanup ([#5666](https://github.com/Hmbown/CodeWhale/issues/5666)) into the release train. A notable fix landed for tool-result batch contiguity ([#5679](https://github.com/Hmbown/CodeWhale/issues/5679)) that eliminates orphaned tool-result images and duplicate tool-call IDs in chat streams. Several UX-focused PRs shipped today, including prompt-based plugin suggestions ([#5663](https://github.com/Hmbown/CodeWhale/issues/5663)) and session boot surfacing for MCP/plugin initialization ([#5658](https://github.com/Hmbown/CodeWhale/issues/5658), rescued in [#5677](https://github.com/Hmbown/CodeWhale/issues/5677)).

---

## 2. Releases

No new releases in the last 24 hours. The v0.9.12 integration branch ([#5576](https://github.com/Hmbown/CodeWhale/issues/5576)) is "gated and code-complete for the release blockers" per maintainer, with version bump and changelog/RC gates remaining.

---

## 3. Hot Issues

**(1) [#5620 — Context pressure warning is transient, agent doesn't proactively react](https://github.com/Hmbown/CodeWhale/issues/5620)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5620)
A medium-severity bug where the context-pressure warning appears briefly and the agent fails to react. **Why it matters:** A silent context-degradation path defeats a critical safety signal. Community: 9 comments, actively discussed. **Reaction:** Users have proposed making the warning sticky and agent-reactive (auto-compaction).

**(2) [#5588 — Provider neutrality: 18 DeepSeek-exclusive gates](https://github.com/Hmbown/CodeWhale/issues/5588)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5588)
Maintainer-lead audit (2,281 lines / 279 files) found 18 behavior gates that are conceptually provider-neutral but hard-coded to DeepSeek. One (NVIDIA NIM env leak) already fixed. **Why it matters:** Impacts multi-provider adoption. Community: 6 comments.

**(3) [#5587 — Dead-code sweep phases 2–4](https://github.com/Hmbown/CodeWhale/issues/5587)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5587)
Continuation of a full audit of 379 `allow(dead_code)` sites: 18 remaining truly-dead items (Tier B/C), ~242 stale allows. **Why it matters:** Reduces compile time and cruft in the main TUI crate. **Reaction:** First slice landed as [#5666](https://github.com/Hmbown/CodeWhale/issues/5666), now closed.

**(4) [#5668 — Add `/copy` for last completed model output](https://github.com/Hmbown/CodeWhale/issues/5668)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5668)
Direct command for copying last assistant output; no manual terminal selection. **Why it matters:** Obvious UX gap for a terminal-based tool; low complexity. Community: 2 comments, enthusiastic.

**(5) [#5617 — Background git probes holding `.git/index.lock`](https://github.com/Hmbown/CodeWhale/issues/5617)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5617)
Internal read-only git probes occasionally block user commits (`index.lock`). **Why it matters:** Breaks the developer workflow entirely. **Reaction:** Fixed and closed; community quickly opened follow-up.

**(6) [#5618 — Replace internal `git` CLI reads with gix (gitoxide)](https://github.com/Hmbown/CodeWhale/issues/5618)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5618)
Follow-up to #5617: move from process-spawning git CLI to pure Rust (gitoxide). **Why it matters:** Eliminates both lock contention and process overhead. Community: 2 comments.

**(7) [#5625 — Non-blocking "pending user input" peek tool](https://github.com/Hmbown/CodeWhale/issues/5625)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5625)
A lightweight tool for mid-turn human-in-the-loop guidance. **Why it matters:** Enhances agent–human collaboration without blocking agent turn. Community: 2 comments (proposal-stage).

**(8) [#5630 — Runtime store owner lock blocks multiple sessions](https://github.com/Hmbown/CodeWhale/issues/5630)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5630)
v0.9.12 integration tree introduced a machine-global single-owner lock causing hard failures. **Why it matters:** Blocks concurrent sessions on one machine. Community: 2 comments; closed (fixed).

**(9) [#5637 — Scope MCP secret providers to owning runtime](https://github.com/Hmbown/CodeWhale/issues/5637)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5637)
Design issue: process-global env mutation for MCP credentials is unsound with multiple threads. **Why it matters:** Security-correctness for embedded hosts. Community: 1 comment (design discussion).

**(10) [#5633 — Unify route-specific tool projection before request dispatch](https://github.com/Hmbown/CodeWhale/issues/5633)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5633)
Provider-specific tool-schema handling scattered across request builders. **Why it matters:** Centralizing improves diagnostics, previews, and correctness. Community: 1 comment.

**(Honorable mention) [#5316 — EPIC-005: CodeWhale TUI Crate Decomposition](https://github.com/Hmbown/CodeWhale/issues/5316)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5316)
Umbrella EPIC with 18 comments, tracking the 620-file monolith decomposition for build-time improvements.

---

## 4. Key PR Progress

**(1) [#5667 — v0.9.12 perf fold and release consolidation](https://github.com/Hmbown/CodeWhale/issues/5667)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5667)
Folds two performance PRs (`#5664`, `#5665`) plus test-only gating (`#5666`); marks Baseten/Groq/Cerebras as "Compatible Hosts"; deletes staged runtime_contract.

**(2) [#5679 — Keep tool result batches contiguous](https://github.com/Hmbown/CodeWhale/issues/5679)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5679)
Fixes tool-result batch integrity: rejects duplicate tool-call IDs, strips orphaned tool results, defers images till batch validation.

**(3) [#5664 — Trim process startup + diagnostic dispatch latency](https://github.com/Hmbown/CodeWhale/issues/5664)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5664)
Removes unused 45-thread tokio runtime in diagnostics; avoids repeated models.dev catalog parsing; parallelizes foreground startup.

**(4) [#5665 — Single-pass token accounting on pressure paths](https://github.com/Hmbown/CodeWhale/issues/5665)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5665)
Fixes multi-pass transcript re-walks per step and repeated streaming re-rendering of accumulated messages.

**(5) [#5677 — Rescue MCP/plugin session boot surfacing](https://github.com/Hmbown/CodeWhale/issues/5677)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5677)
Rescues #5658 onto `main`: surfaces plugin discovery + MCP servers as session boot state; fixes the "`working · 22s · 0 steps`" cold-start UX.

**(6) [#5663 — Suggest plugins from the prompt](https://github.com/Hmbown/CodeWhale/issues/5663)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5663)
Ranks prompt against installed plugins; toasts next step when matches found — no manual `/plugin suggest` required.

**(7) [#5666 — Gate audited test-only helpers](https://github.com/Hmbown/CodeWhale/issues/5666)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5666)
Converts 13 audited test helpers from `#[allow(dead_code)]` to `#[cfg(test)]`; first slice of #5587.

**(8) [#5658 — Surface MCP/plugin boot as session set](https://github.com/Hmbown/CodeWhale/issues/5658)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5658)
Original (pre-rescue) PR: names connecting servers on first session frame, persists failure state, includes canonical "use /mcp" text.

**(9) [#5669 — Update nixpkgs with monthly dependabot](https://github.com/Hmbown/CodeWhale/issues/5669)** · [Closed](https://github.com/Hmbown/CodeWhale/issues/5669)
Fixes `nix run` 403 errors; modernizes `stdenv.isLinux` references; adds automated monthly nixpkgs updates.

**(10) [#5676 — Dependabot: futures-util 0.3.33 → 0.3.34](https://github.com/Hmbown/CodeWhale/issues/5676)** · [Open](https://github.com/Hmbown/CodeWhale/issues/5676)
Routine dependency bump; preserves cloned wakers.

---

## 5. Feature Request Trends

**📌 UX/Interaction parity with Claude Code** — Strong recurring theme across the 0.9.12 cycle ([#5579](https://github.com/Hmbown/CodeWhale/issues/5579)): proactive plugin recommendations (`#5663`), reload discoverability, hot-reload. The focus is entirely on **session-surface discoverability** rather than hidden commands.

**📌 Terminal copy/selection ergonomics** — The `/copy` request (`#5668`) joins a series of per-block actions (`#5551`: y/Y/fullscreen/raw-markdown) — clearly a directional push to reduce manual terminal selection friction.

**📌 Build/latency performance as product surface** — `#5620` (context pressure), `#5633` (tool projection), and `#5625` (non-blocking user input) all address **turn-time intelligence**: helping the agent (and the user) understand *what the agent is doing right now*. Diagnostics and latency transparency are treated as UX features, not just ops issues.

**📌 Cross-provider neutrality** — `#5588` (18 DeepSeek-exclusive gates), `#5633`, and `#5637` all point toward making the tool equally strong on non-DeepSeek backends.

---

## 6. Developer Pain Points

**♦️ Git CLI process spawning** — Two consecutive issues (`#5617` closed, `#5618` open) highlight real pain: internal git probes cause repository lock failures and ~60% worse performance than direct read operations. The fix (moving to gitoxide) is clearly desired by the community — it's not just about correctness, it's about speed.

**♦️ Silent/transient safety signals** — `#5620` captures a deeper frustration: the tool's warnings are **transient and non-actionable**. The community wants the agent to *react* to pressure, not just display a flash; "silent context degradation" is a recurring theme.

**♦️ Build-time monolith tax** — `#5249` (EPIC: 620-file crate, 86% of workspace, recompile-as-one-unit) remains open. Every commit invalidates the SHA stamp; every test invokes 25 integration binaries. The community sees this as a top-level reliability and velocity blocker — hence the decomposition EPIC (`#5316`).

**♦️ Multi-session / multi-process management** — `#5630` (runtime store owner lock) and `#5637` (secret-store scoping) both spotlight that single-machine concurrency is underspecified: users run multiple sessions, multiple hosts, and the platform must not assume global exclusivity.

---

*Digest generated from public GitHub data. All links point to the [Hmbown/CodeWhale repository](https://github.com/Hmbown/CodeWhale).*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*