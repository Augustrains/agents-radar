# AI CLI Tools Community Digest 2026-08-01

> Generated: 2026-08-01 01:27 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report
**Date: 2026-08-01**

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is in a critical maturation phase, marked by an intense focus on reliability, safety, and resource management. Seven major tools (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI/CodeWhale) are actively iterating, with **Claude Code, Codex, and Gemini CLI** leading in community engagement and GitHub activity. **Safety incidents** — including multiple catastrophic `rm -rf` data-loss events (Claude Code) and credential leakage — dominate the most urgent discussions, signaling that developer trust is the industry's primary battleground. **Session state management** (persistence, resume, cross-machine continuity) and **resource governance** (memory limits, quota tracking, context window management) are emerging as universal differentiators. The rapid-release cadence across tools (multiple alpha releases daily for Codex, patched stable releases for Gemini CLI) reflects both healthy iteration and **regression churn** that is increasingly frustrating users.

---

## 2. Activity Comparison (2026-08-01)

| Tool | Community Issues (Hot/Active) | PRs (24h) | Release Status (24h) | Notable Signals |
|------|------|------|------|------|
| **Claude Code** | 10 hot issues; 83 max 👍 | 6 PRs updated | No new release | Highest severity: `rm -rf` incidents, billing misalignment |
| **OpenAI Codex** | 10 hot issues; 185 max 👍 | 10+ merged/updated | 3 alpha releases | Very high engagement on auto-resolve setting (#28969) |
| **Gemini CLI** | 8 hot issues + 2 PRs; 8 max 👍 | 10 PRs | 2 releases (v0.53.1, v0.54.0-preview.1) | Regression churn in v0.53.0; capacity-exhaustion fixes |
| **GitHub Copilot CLI** | 10 hot issues; 6 max 👍 | 2 PRs (low-quality) | v1.0.78-0 (Jul 31) | 2 regressions closed this week; resume-performance regression open |
| **Kimi Code CLI** | 4 active discussions | 1 PR (high-impact fix) | No new release | Long-running feature gaps (Remote Control, Memory) |
| **OpenCode** | 10 hot issues; 20 max 👍 | 10+ PRs (mostly dead-code cleanup) | No new release | Managed service (Go/Zen) outage — 401s — top concern |
| **Pi** | 10 hot issues; 5 max 👍 | 10 PRs (server/session focus) | No new release | Server-mode architecture push; CPU-compat regression |
| **Qwen Code** | 10 hot issues; 31 max comments | 10+ PRs | v0.21.2 | Autofix maturity; multi-workspace daemon RFC |
| **DeepSeek TUI (CodeWhale)** | 10 hot issues; 5 max comments | 8 PRs (incl. 5 dependabot) | v0.9.3 | Rebranding to CodeWhale; community-contributed fixes |

**Release velocity leaders:** OpenAI Codex, Gemini CLI, Qwen Code, Copilot CLI. **Community engagement leaders:** Claude Code, Codex, Gemini CLI.

---

## 3. Shared Feature Directions

| Feature Direction | Tools | Specific Needs |
|------------------|-------|----------------|
| **Session persistence & cross-machine resume** | Claude Code (#31992), Codex, Gemini CLI, Kimi CLI (#1282), Pi (server-mode PRs), CodeWhale (#5000) | Syncable transcripts; durable partial output; CLI-to-CLI handoff; web/cloud companion; remote session control |
| **Resource governance & quota transparency** | Claude Code (#79337), Codex (#36353, #36396, #35259), Gemini CLI (#28566), Qwen Code (#8051, #8182) | Accurate billing logic; no idle-token burns; memory budgets per agent/child; visible rate-limit status |
| **Context/compaction reliability** | Claude Code (#83019), Gemini CLI (#26522), Pi (#6879, #7253, #7020), OpenCode (#23595), Qwen Code (#6721) | Auto-compact after every turn; no O(n²) JSON logs; avoid double-compaction; preserve interrupted output; prevent cache busting |
| **Subagent transparency & control** | Claude Code (#74113), Codex (#36396), Gemini CLI (#22323, #21409), Qwen Code (#7835), Copilot CLI (#4161) | Force-resume capability; explicit success/failure semantics; subagent trajectory visibility; user-question forwarding; config-respecting execution |
| **Safety-guard hardening** | Claude Code (#81273, #82165, #74422), Gemini CLI (#28557 SSRF), Qwen Code (#8227 O_NOFOLLOW) | No `rm -rf` bypasses; sandbox kill attempts not blocked; path-allowlists (CodeWhale #5005); SSRF protection; symlink TOCTOU guards |
| **Enterprise/org policy management** | Copilot CLI (#3909), OpenCode (#39875), Codex (#35006) | Centralized config/Env vars; predictable OAuth lifecycle; explicit telemetry/retention policies; provider attribution |
| **ACP/agent-interop depth** | Codex (#36413, #36410), Copilot CLI (#2109), CodeWhale (#4996, #4997), OpenCode (#17505) | Structured user-questioning; delegation acknowledgements; protocol-neutral clients; external ACP worker backends |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Highlight | Key Differentiator |
|------|--------------|-------------|--------------------|--------------------|
| **Claude Code** | Agentic safety, TUI stability, web integration | Enterprise devs on Max/Pro plans | Fable 5 model gating; auto-mode guardrails | **Safety-first positioning** — but incidents (rm -rf) undermine claims |
| **OpenAI Codex** | Rust SDK, app-server architecture, ACP extensibility | IDE-power users, macOS/Windows devs, SDK integrators | Sandboxed V8 for code mode; thread-section management; strict automatic review | **Rapid SDK iteration** + delegation: alpha releases daily; ACP parity |
| **Gemini CLI** | Stable agent execution, OAuth security, subagent reliability | Google-ecosystem devs, GHE enterprise | Capacity-exhaustion classification; SSRF fix; thoughtSignature preservation | **Controlled stable/preview release lines** — two-track releases reduce regression blast radius |
| **Copilot CLI** | Enterprise CI/automation, sandboxed builds, plan/review modes | GitHub-centric devs, org admins | ACP closeSession; /permissions command; dev-tool caches | **Management-plane focus** — org-managed settings request (still open) signals enterprise pull |
| **Kimi Code CLI** | Lightweight cross-provider CLI, feature discovery | Devs who switch model backends | Recursive JSON-unwrapping fix for multi-provider reliability | **Bare-bones CLI** — no release in 24h; community clamors for memory + remote control |
| **OpenCode** | TUI ergonomics, plugin ecosystem, local-LLM support | Local-model tinkerers, plugin authors, ACP integrators | Dead-code cleanup wave; plugin watch; transparency toggle | **TUI polish priority** — black-screen regressions since Nov 2025 remain a trust gap; Go/Zen service instability |
| **Pi** | Server-mode architecture, parallel tool integrity, provider breadth | Multi-provider power users, WSL/GPU users, server ops | Composable protocol server; durable session locks; JSON delta streaming | **Server/headless direction** — christianklotz PR cluster signals first-class remote sessions; CPU-compat regression addressed |
| **Qwen Code** | Autofix, daemon multi-workspace, web-shell maturity | Qwen-model power users, CI autofix pipelines | Memory-budget reporting; Goal v3 TUI integration; round-limit autofix | **Production daemon focus** — multi-workspace resource bounding RFC is largest community discussion this week |
| **DeepSeek TUI/CodeWhale** | DeepSeek V4 Flash, TUI rendering fidelity, i18n | DeepSeek local/API users, CJK-language devs | File-edit diagnostics; AltGr key fix; canonical tool catalog | **Rebranding moment** — from niche TUI to CodeWhale; community-contributed fixes dominate; benchmark-harness demands signal growing rigor |

---

## 5. Community Momentum & Maturity

**Most active & maturing:** **Claude Code** remains the most engaged community (high upvotes, deep issue threads) but is suffering from **trust erosion** — four catastrophic data-loss issues and billing confuse signals are its top signals. **OpenAI Codex** is the fastest-iterating (3 alpha releases in 24h) with a very high-engagement feature request (#28969 at 185 👍), indicating a healthy feedback loop. **Gemini CLI** shows a stable two-track release cadence with active backports — a sign of disciplined engineering, though regression churn (thoughtSignature) tests patience.

**Rapidly iterating with growing rigor:** **Qwen Code** is pivoting to production-grade daemon management (RFC #6378, memory-budget PRs). **Pi** is investing heavily in server-mode architecture (5+ PRs in 24h) — an outlier in committed engineering bandwidth. **Copilot CLI** is maturing but shows **low PR activity** (2 low-quality PRs) — the community is vocal, but maintainer bandwidth appears constrained.

**Emerging/challenged:** **OpenCode** faces a community trust crisis (Go/Zen 401 outage, privacy-policy backlash) despite a healthy PR cleanup wave. **Kimi Code CLI** is quiet (no release in 24h) with no maintainer-driven feature velocity — but a high-impact PR (#2572) addressing a systemic bug class is now open. **CodeWhale** is in a **rebranding transition** with high community contribution (2 significant community PRs accepted in the release train) — momentum is positive but small-scale.

**Maturity rubric:**
- **Safety posture:** Claude Code (worst), Gemini CLI (improving — SSRF fix), Codex (hardening — v8 sandbox), Qwen Code (improving — O_NOFOLLOW).
- **Release discipline:** Gemini CLI (best — cherry-pick backports), Codex (fast — daily alphas), Copilot CLI (medium — weekly), Claude Code (least active — no release in 24h).

---

## 6. Trend Signals

1. **The "Safety Tax" is real.** Multiple tools (Claude Code, CodeWhale, Qwen Code, Gemini CLI) are either shipping safety fixes or exposing safety gaps. Developers are treating guardrail bypasses as **P0 security bugs**, not quality nits — expect safety to become a checklist item in procurement decisions.

2. **Session state is the new "saved game."** Cross-machine resume (#31992 in Claude Code, #1282 in Kimi CLI), durable partial output (#5000 in CodeWhale), and server-mode sessions (Pi PR cluster) all point to **session continuity as a core UX expectation**, not a nicety.

3. **Context windows are a scaling wall.** Every tool community reports pain with context bloat: O(n²) JSON output (Pi), image resends (Codex), prompt-cache busting (OpenCode, Qwen Code), and compaction misfires (Pi, Gemini CLI). Expect **agent-compaction heuristics and delta-streaming protocols** to become competitive differentiators in the coming quarters.

4. **Rate/credit accounting erodes trust fastest.** Billing confusion (Claude Code Max vs. Fable 5), weekly-quota mis-accounts (Codex), and idle-token burns (Codex's wait/status polling, Gemini's capacity retries) are top-engagement issues across tools. **Transparent, configurable usage visibility is table stakes** — tools that can't show where credits go will lose power users.

5. **The ACP/interop wave is building.** Codex (delegation ack, strict auto-review), Copilot CLI (ACP closeSession, ask_user demand), CodeWhale (protocol-neutral ACP client, Copilot-as-backend), and OpenCode (ACP timing bugs) all signal **the industry moving toward multi-agent orchestration** where CLI tools become pluggable workers, not islands.

6. **Windows and WSL remain the weakest link.** WSL login hangs (Pi), Git detection breaks (Codex), AltGr key collisions (CodeWhale), MSIX corruption (Claude Code), PATH truncation (CodeWhale) — **Windows is the second-class citizen in every tool**. Developers targeting corporate Windows environments should weigh this heavily.

7. **Local-LLM integration is a "long tail" differentiator.** OpenCode (cache busting, tool-call parsing), Pi (Baseten provider, Bedrock Mantle), Qwen Code (qwen3.7-max plain-text drift), and CodeWhale (DeepSeek V4 Flash) all attract niche but passionate communities. **Tools that nail local/cloud hybrid workflows** (Codex's NPU proposal #22041) could capture the prosumer segment.

---

## Bottom Line for Decision-Makers

- **For enterprise safety-critical use:** Gemini CLI and Qwen Code are investing most in security hardening; Claude Code's data-loss incidents should trigger extra scrutiny of guardrail design.
- **For IDE-heavy workflows:** Codex (macOS) and Copilot CLI (enterprise GitHub) are the most aligned, though both have platform-specific regressions.
- **For server/headless deployments:** Pi's server-mode PR cluster and Qwen Code's daemon RFC are the most forward-looking — but both are pre-production.
- **For multi-provider flexibility:** Kimi CLI's JSON-unwrapping fix and CodeWhale's canonical tool catalog are the most promising, but both have small maintainer capacity.
- **Watch closely:** OpenCode's Go/Zen outage resolution and Claude Code's next release (no release in 24h is anomalous for a tool with this user base) will likely shape sentiment in the next 48–72 hours.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-08-01 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking (Most-Discussed PRs)

### #514 — document-typography
**Typographic quality control for generated documents**
- **Function:** Prevents orphan word wrap, stranded widow paragraphs, and numbering misalignment in AI-generated documents — issues that affect every document Claude produces.
- **Discussion:** Centered on the universal pain point of AI document formatting; maintainers engaged on trigger precision.
- **Status:** Open (since March 2026). [View PR](https://github.com/anthropics/skills/pull/514)

### #523 — skill-creator fix: run_eval.py always reports 0% recall
**Critical bugfix cluster (multiple PRs: #1298, #1099, #1050, #1323, #1261)**
- **Function:** Fixes the skill-description optimization loop reporting `recall=0%` on every query due to trigger-detection failures, Windows subprocess incompatibilities (`PATH EXT` not honored, `cp1252` encoding, `select` on pipes), and synthetic command files leaking into live project registries.
- **Discussion:** The single highest-velocity thread in the repo. Ten+ independent reproductions (#556) across Windows/Linux. Multiple contributors (MartinCajiao, joshuawowk, gstreet-ops, Polluelo978, alvingarcia, Lubrsy706) converged on overlapping root causes. Community consensus: the eval harness is currently "optimizing against noise."
- **Status:** All Open; multiple parallel fix attempts. [View PR #1298](https://github.com/anthropics/skills/pull/1298) | [#1099](https://github.com/anthropics/skills/pull/1099) | [#1050](https://github.com/anthropics/skills/pull/1050) | [#1323](https://github.com/anthropics/skills/pull/1323) | [#1261](https://github.com/anthropics/skills/pull/1261)

### #486 — ODT skill
**OpenDocument text creation, template filling, and ODT→HTML parsing**
- **Function:** Full OpenDocument Format (.odt, .ods) support — create, fill templates, read, and convert. Triggers on "ODT," "ODS," "ODF," "OpenDocument," "LibreOffice."
- **Discussion:** Highlights the gap in office-format coverage (DOCX exists; ODT doesn't). Useful for EU/government environments standardizing on ODF.
- **Status:** Open (since March 2026). [View PR](https://github.com/anthropics/skills/pull/486)

### #541 — fix(docx): tracked change w:id collision
**Document corruption fix for DOCX skill**
- **Function:** Fixes `w:id` collisions when adding tracked changes to documents with existing bookmarks — a shared ID space in OOXML that corrupted output with hardcoded low IDs.
- **Discussion:** Demonstrates the community's attention to low-level OOXML correctness; actively maintained author (Lubrsy706).
- **Status:** Open. [View PR](https://github.com/anthropics/skills/pull/541)

### #1302 — color-expert
**Self-contained color-expertise skill**
- **Function:** Comprehensive color knowledge — naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912), color spaces with a "what-to-use-when" table (OKLCH for scales, OKLAB for gradients, CAM16 for perception).
- **Discussion:** Strong enthusiasm from design-adjacent users; still active after 6 weeks.
- **Status:** Open (since June 2026). [View PR](https://github.com/anthropics/skills/pull/1302)

### #1367 — self-audit
**Mechanical verification + four-dimension reasoning quality gate**
- **Function:** Pre-delivery audit: Step 0 verifies every claimed output file exists; then four-dimension reasoning audit in damage-severity priority order. Universal across tech stacks.
- **Discussion:** Unique positioning — not domain-specific but a meta quality check. Related issue proposal #1385 extends to a three-gate pipeline.
- **Status:** Open (since June 2026, v1.3.0). [View PR](https://github.com/anthropics/skills/pull/1367)

---

## 2. Community Demand Trends (from Issues)

### Highest-Intensity Demand: Fixing the skill-creator eval loop (#556 — 12 comments, 7 👍)
The most-downloaded pain point. `run_eval.py` reports **0% recall across all queries**, breaking description optimization entirely. Ten+ independent reproductions, Windows-specific subprocess failures, and command-file isolation problems. This is a **blocker for the entire skills-development workflow** — the ecosystem's own tooling is broken.

### Security & Trust Boundary Abuse (#492 — 43 comments, 2 👍)
**The most-commented issue in the repo.** Community skills distributed under the `anthropic/` namespace impersonate official skills, creating a trust-boundary vulnerability where users grant elevated permissions to unofficial skills. Escalated concern with active maintainer discussion — likely to drive namespace/packaging governance changes.

### Organizational Skill Sharing (#228 — 16 comments, 8 👍)
Skills should be shareable within organizations (workspace-level libraries, direct share links) instead of manual `.skill` file distribution via Slack/Teams. Clear enterprise demand signal.

### Skill-Plumbing Bugs
**Duplicate skills across plugins** (#189 — 9 👍): `document-skills` and `example-skills` contain identical content, inflating context. **claude-api skill injects ~156k tokens** (#1487) — exhausting context in a single tool call. Both point to a need for **skill deduplication and lazy-loading**.

### Emerging Demand: Governance & Reasoning Quality
**agent-governance** (#412): safety patterns for policy enforcement and audit trails. **Reasoning Quality Gate Pipeline** (#1385): pre-task calibration → adversarial review → delivery verification. A cluster of users is pushing toward **AI-output reliability layers**, not just format-handling skills.

---

## 3. High-Potential Pending Skills (Active, Unmerged)

These PRs have active discussion, multiple revisits, and are likely to land within weeks:

| PR | Skill | Why It's Likely to Land |
|---|---|---|
| [#486](https://github.com/anthropics/skills/pull/486) | **ODT** — OpenDocument support | Fills an obvious format gap (DOCX exists, ODT doesn't); EU public-sector ODF requirement is a strong pull |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** — full testing stack incl. Testing Trophy, AAA, React Testing Library | Makes Claude a competent testing partner; very high practical leverage |
| [#525](https://github.com/anthropics/skills/pull/525) | **pyxel** — retro game dev via MCP | Self-contained, well-scoped, references a specific MCP server; low friction to merge |
| [#1367](https://github.com/anthropics/skills/pull/1367) | **self-audit** — reasoning quality gate | Response to the strongest community pain (unreliable AI output); actively iterating v1.3.0 |
| [#1479](https://github.com/anthropics/skills/pull/1479) | **plan-file-hygiene** — planning artifact lifecycle | Addresses #1417 (planning files accumulate with no lifecycle); community co-designed |
| [#1302](https://github.com/anthropics/skills/pull/1302) | **color-expert** | High-quality, self-contained expertise skill; zero external deps |
| [#539](https://github.com/anthropics/skills/pull/539) | **skill-creator fix** — unquoted YAML description warnings | Small, safe, targeted fix to the core toolchain |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, Windows-portable skill-development toolchain (fixing `run_eval.py`'s systemic 0%-recall failures) and for security/governance safeguards against namespace spoofing — before domain-specific skill breadth becomes the dominant concern.**

---

*Report generated from anthropics/skills public activity data (2025-10 through 2026-08).*

---

# Claude Code Community Digest
**2026-08-01**

---

## Today's Highlights

No new releases shipped in the past 24 hours, but the community is actively surfacing critical reliability and safety concerns. The most pressing issues revolve around **Fable 5 access/billing discrepancies on Max plans**, a series of **catastrophic `rm -rf` data-loss incidents** where safety guards were bypassed, and **session state loss** (transcripts, quota consumption, model fallbacks). Several new bug reports today point to subtle but impactful configuration sync issues, including sandbox escapes and plugin starvation across projects.

---

## Releases

*No new releases in the last 24 hours.*

---

## Hot Issues

Here are 10 issues generating the most community engagement and concern:

### 1. Fable 5 prompts 'usage credits required' on Max plan
**#79337** | 👍 20 | 💬 51 | [Link](https://github.com/anthropics/claude-code/issues/79337)
On the day Fable 5 became standard on Max plans, Claude Code refuses to run it, silently downgrading to Opus 4.8 and demanding usage credits. This is the **highest-comment issue** right now, with a related duplicate (#79441) reporting the same problem in VS Code even with 20% weekly allowance remaining. **Why it matters:** Billing/auth logic is misaligned with plan entitlements, eroding trust in Max plan value.

### 2. Scroll wheel no longer scrolls conversation — sends arrow keys instead
**#65833** | 👍 83 | 💬 35 | [Link](https://github.com/anthropics/claude-code/issues/65833)
Regression in v2.1.150 on WSL: mouse wheel cycling through input history instead of scrolling output. **Why it matters:** Long-standing TUI regression (open since June) with broad community support — 83 upvotes signals significant daily workflow disruption.

### 3. Claude Code Web Cannot Use gh CLI Commands (Permission Denied)
**#11139** | 👍 31 | 💬 28 | [Link](https://github.com/anthropics/claude-code/issues/11139)
Ongoing issue (since Nov 2025) blocking GitHub CLI usage in the web environment; labeled `oncall`. Recently updated again, keeping it on the radar. **Why it matters:** Web-based workflows remain incomplete without full toolchain access.

### 4. GPU process crash kills Claude Desktop and corrupts MSIX package
**#81159** | 👍 0 | 💬 9 | [Link](https://github.com/anthropics/claude-code/issues/81159)
When Opus 5 performs an in-page browser action on Windows 11, the GPU process crashes (exitCode 101457950), killing the entire desktop app and corrupting its MSIX package. **Why it matters:** Severe stability bug — desktop app becomes unusable and may need reinstall.

### 5. Cross-session credential leakage: production database modified on unauthorized host
**#72274** | 👍 1 | 💬 6 | [Link](https://github.com/anthropics/claude-code/issues/72274)
Another user's production server credentials surfaced in the reporter's session, leading to unauthorized database modification. **Why it matters:** Credential leakage across sessions is a critical security failure — potentially indicative of shared state or sandbox isolation issues.

### 6. Background agents go idle without delivering final SendMessage report
**#74113** | 👍 5 | 💬 5 | [Link](https://github.com/anthropics/claude-code/issues/74113)
On Windows, background agents frequently go idle without completing their final report; re-pinging recovers it. **Why it matters:** Unreliable agent completion breaks automation and CI pipelines.

### 7. Fable 5 safeguards over-flag legitimate defensive security audit workflows
**#74422** | 👍 0 | 💬 2 | [Link](https://github.com/anthropics/claude-code/issues/74422)
Routine defensive security-audit workflows (authorized repo audits, gitleaks/deps/vuln review) are blocked by Fable 5 safeguards. **Why it matters:** Overly aggressive safety filters block legitimate use cases, creating friction for security professionals.

### 8. Auto-mode catastrophic-removal guard bypassed: `rm -rf` in backtick substitution
**#81273** | 👍 0 | 💬 1 | [Link](https://github.com/anthropics/claude-code/issues/81273)
The auto-mode destructive-command guard is bypassed when `rm -rf` is embedded in a backtick substitution — executes without confirmation. **Why it matters:** Safety guard circumvention is a serious, exploitable weakness.

### 9. Catastrophic data loss: agent-built command expanded to "rm -rf /*", ran detached
**#82165** | 👍 0 | 💬 1 | [Link](https://github.com/anthropics/claude-code/issues/82165)
Fable 5 constructed a cache-clearing command that expanded to `rm -rf /*`, ran it detached, and then the safety classifier blocked kill attempts. **Why it matters:** The worst-case scenario: total system loss, compounded by the safety system preventing remediation.

### 10. Session transcripts auto-delete after 30 days — silent, permanent loss of project history
**#83019** | 👍 0 | 💬 1 | [Link](https://github.com/anthropics/claude-code/issues/83019)
Session transcripts default to a location outside typical backup coverage and auto-delete after 30 days. **Why it matters:** Silent, permanent loss of project context and historical decisions.

---

## Key PR Progress

Six PRs were updated in the last 24 hours. The notable ones:

### 1. Fix #80705: Usage leak problem
**#81540** | [Link](https://github.com/anthropics/claude-code/pull/81540)
Automated contribution (by "Atlas 2") closing a usage leak bug with a stated $200 reward. Closed but notable for the automated contribution approach.

### 2. docs: add README.md for security-guidance plugin
**#17776** | [Link](https://github.com/anthropics/claude-code/pull/17776)
Adds comprehensive documentation for the security-guidance plugin, covering all 9 security patterns. Small but valuable documentation improvement.

### 3. fix(ci): fix cron failures, exclude PRs, and propose TUI latency fix
**#82987** | [Link](https://github.com/anthropics/claude-code/pull/82987)
Addresses GitHub Actions cron failures and proposes an architectural fix for **TUI input latency degradation under high agent workloads** — directly responding to community complaints about TUI responsiveness.

### 4. feat(code-review): implement confidence scoring and --threshold flag
**#82794** | [Link](https://github.com/anthropics/claude-code/pull/82794)
Implements the documented 0–100 confidence scoring for the code-review plugin (previously binary), reconciling README↔command drift. *Note: This is a community plugin PR, not core Claude Code.*

### 5. Upgrade Node.js version from 20 to 24
**#39872** | [Link](https://github.com/anthropics/claude-code/pull/39872)
Long-pending dependency upgrade (open since March) for the upcoming LTS change.

### 6. Claude/automatizar inventario insumos w4n98s
**#82981** | [Link](https://github.com/anthropics/claude-code/pull/82981)
Unrelated/accidental PR (Spanish-language inventory automation), likely a mistaken submission.

---

## Feature Request Trends

Distilling feature directions from recent issues:

1. **Cross-machine session resume** (#31992): Sync session state for CLI-to-CLI handoff across machines — a top community desire for seamless workflow portability.

2. **Advisor agent force-resume** (#83014): Ability for the advisor agent to force-resume failed agent processes, reducing wasted time from API-error deaths.

3. **CLI retrieval of backgrounded cloud session results** (#83012): No current way for a CLI session to pull results from a backgrounded Ultraplan/cloud session without manual browser steps.

4. **Bash tool under actual bash** (#74746): Community wants the Bash tool to honor bash semantics, not the user's login shell (zsh) — reducing command breakage on bash-vs-zsh differences.

5. **Plugin sync per-project** (#83034): The `enabledPlugins` → `installed_plugins.json` sync should be keyed on `(key, projectPath)` not just plugin key, preventing plugin starvation after the first project.

---

## Developer Pain Points

Recurring frustrations from the community:

1. **Fable 5 billing/access confusion** — Multiple reports of usage-credit errors despite Max plan coverage. The silent downgrade to Opus 4.8 compounds the confusion.

2. **Catastrophic data-loss incidents** — No fewer than **four separate issues** (#75794, #80830, #81273, #82165) report destructive `rm -rf` execution without confirmation, including safety-guard bypasses and cases where the safety classifier blocks remediation. This is the most urgent pain point.

3. **Session state fragility** — Silent model fallbacks (Fable 5 → Sonnet 5) without notice (#83036), lost output despite quota consumption (#83001), and 30-day transcript auto-deletion (#83019) all contribute to a sense of unreliability.

4. **Configuration drift and silent drops** — Sandbox configs silently dropped for nested project directories (#83035), plugin sync gated incorrectly (#83034), and IDE selection leakage from closed unsaved files (#71566) — all indicate configuration handling is a systemic weakness.

5. **Korean/Hangul corruption in tool-call parameters** — Root-caused by Sonnet 5 writing `\uXXXX` escapes with mis-spelled hex (#83033), corrupting Hangul 100% when triggered. Affects non-English-language users disproportionately.

6. **Web/cloud environment gaps** — GitHub CLI permission issues (#11139) and Gradle proxy failures (#16222) continue to limit web-based workflows.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-01

## Today's Highlights
Three rapid-fire alpha releases (`rust-v0.147.0-alpha.1.1` through `.alpha.4`) landed in the last 24 hours, signaling active iteration on the Rust SDK. Community attention remains focused on two fronts: rate-limit/credit exhaustion concerns (at least five new issues) and platform-specific reliability bugs on Windows and macOS. A notable cluster of merged PRs around thread-state management, plugin search APIs, sandboxed V8 for code mode, and explicit user-input semantics suggests the team is prioritizing architectural hardening alongside new delegation and approval features.

## Releases
**No changelog details available for the three latest releases:**
- [rust-v0.147.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.4)
- [rust-v0.147.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.3)
- [rust-v0.147.0-alpha.1.1](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1.1)

All three are tagged as "Release 0.147.0-alpha.*" with no accompanying release notes. Developers should monitor the repository for updated documentation or migration guides.

## Hot Issues

1. **[#28969 — Add setting to disable 60-second auto-resolve for questions](https://github.com/openai/codex/issues/28969)** (185 👍, 64 comments)  
   The most-engaged open issue this week. Users want control over Codex's automatic resolution of questions after 60 seconds. High upvote count signals strong demand for manual override.

2. **[#35058 — Codex Diff crashes with "Oops, an error has occurred" in VS Code on macOS](https://github.com/openai/codex/issues/35058)** (109 👍, 42 comments)  
   A blocking regression for macOS Apple Silicon users. Codex Diff tab is completely unusable across repositories — a critical IDE workflow breaker.

3. **[#34133 — Windows GPU process crash on screenshot due to Code Integrity rejecting vk_swiftshader.dll](https://github.com/openai/codex/issues/34133)** (30 comments)  
   In-app Browser screenshots crash the GPU process, causing freezes and failure to reopen. Windows 10 enterprise environments with Code Integrity enforcement are particularly affected.

4. **[#30408 — MCP server processes leak (9+ GB RSS)](https://github.com/openai/codex/issues/30408)** (21 comments)  
   App-server spawns full MCP server process sets per thread and never cleans them up when threads close. Unbounded memory growth is observed over time.

5. **[#35119 — Windows/WSL valid repos marked as non-Git, "Git is unavailable"](https://github.com/openai/codex/issues/35119)** (11 comments, 11 👍)  
   The latest Windows unified app build regresses WSL2 repository detection. Valid ext4 WSL repos are treated as non-Git, breaking core workflows; previous build worked.

6. **[#36353 — Weekly quota exhausted in <24 hours on ChatGPT Plus](https://github.com/openai/codex/issues/36353)** (6 comments)  
   Fresh complaint about possible incorrect weekly usage accounting. Users report the full weekly Codex allowance disappears overnight without heavy usage.

7. **[#28316 — Avoid resending large base64 images in later context](https://github.com/openai/codex/issues/28316)** (10 comments)  
   Codex persists full base64 image payloads in tool history and re-sends them on subsequent `/v1/responses` calls, causing unbounded context bloat and unnecessary token spend.

8. **[#35259 — Desktop re-enters model during wait/status polling, consuming credits](https://github.com/openai/codex/issues/35259)** (9 comments)  
   Model turns whose only tool action was wait/status polling accounted for 19.8% of raw token volume. Rate-limit and credit waste from idle polling.

9. **[#32250 — GPT-5.6 Sol Medium depletes Pro 5-hour allowance quickly](https://github.com/openai/codex/issues/32250)** (8 👍)  
   Pro users report the Medium reasoning effort on GPT-5.6 Sol burns through the usage window far faster than expected. Concerns about cost-effectiveness of the mode.

10. **[#36396 — Sub-agent busy-waiting burns a week of quota (6,932 blocking waits)](https://github.com/openai/codex/issues/36396)** (2 comments)  
    A single 11-day session consumed 71% of total token usage — with 23.7% of 6,932 blocking waits returning empty. Illustrates systemic waste in the sub-agent polling design.

## Key PR Progress

1. **[#36413 — Add realtime delegation acknowledgement control](https://github.com/openai/codex/pull/36413)**  
   New optional `delegationAckFiller` field for `thread/realtime/start`, forwarded as `delegation.ack_filler` to V3 Frameless Bidi sessions.

2. **[#36410 — Make user input blocking behavior explicit](https://github.com/openai/codex/pull/36410)**  
   Adds required `isBlocking` to `request_user_input`, decoupling the blocking decision from `autoResolutionMs` timeout policy.

3. **[#36409 — Implement remote plugin search](https://github.com/openai/codex/pull/36409)**  
   `plugin/search` queries remote plugin service without catalog cache; supports global/workspace/personal scopes with cursors and feature gates.

4. **[#36389 — Enforce single-writer ownership for all thread histories](https://github.com/openai/codex/pull/36389)**  
   Extends cross-process writer lock to legacy thread histories, preventing concurrent-write corruption.

5. **[#36373 — Add `--approve-for-me` CLI flag](https://github.com/openai/codex/pull/36373)**  
   Routes approval requests through automatic review for interactive and exec commands; configures `approval_policy="on-request"` + `workspace-write` sandbox.

6. **[#36374 — Enable sandboxed V8 for code mode](https://github.com/openai/codex/pull/36374)**  
   Enables `v8_enable_sandbox` feature for code mode, fixing Windows MSVC non-sandboxed prebuilts and package build profile selection.

7. **[#36365 — Add strict automatic review for MCP elicitations](https://github.com/openai/codex/pull/36365)**  
   Recognizes `codex_strict_auto_review` MCP elicitation marker; routes marked approvals to automatic reviewer and fails closed without user prompt.

8. **[#36380 — Add thread section management APIs](https://github.com/openai/codex/pull/36380)**  
   New `threadSection/create`, `/update`, `/delete` app-server methods with SQLite persistence (UUIDv7 IDs) and validation.

9. **[#36384 — Load turn summaries with paginated queries](https://github.com/openai/codex/pull/36384)**  
   Eliminates N+1 item queries in summary view by joining first user and final agent items into the paginated turn query.

10. **[#36367 — Keep effective tool exposure in the registry](https://github.com/openai/codex/pull/36367)**  
    Stores each runtime alongside its effective exposure in `ToolRegistry`, preserving step-specific policy applied by hosts.

## Feature Request Trends

- **User control over auto-resolution** ([#28969](https://github.com/openai/codex/issues/28969)): Request to disable or configure the 60-second auto-resolve for questions. Very high engagement (185 👍).
- **Dynamic sub-agent naming** ([#29649](https://github.com/openai/codex/issues/29649), [#19186](https://github.com/openai/codex/issues/19186)): Sub-agents should use user-defined or task-derived names rather than forced runtime nicknames for clarity in role-based workflows.
- **Hybrid local/cloud "Instant" models** ([#22041](https://github.com/openai/codex/issues/22041)): Proposal to use Apple/Intel/AMD NPUs for lightweight local inference to complement cloud models.
- **Reliable MCP OAuth and reauthentication** ([#35006](https://github.com/openai/codex/issues/35006)): Enterprise SSO users want a dependable OAuth lifecycle — umbrella issue tracking several narrower bug reports.
- **PR template support in Codex Cloud** ([#17932](https://github.com/openai/codex/issues/17932), [#6750](https://github.com/openai/codex/issues/6750)): Codex Cloud "Create PR" should respect `.github/pull_request_template.md` like the CLI does.

## Developer Pain Points

- **Rate-limit and quota exhaustion dominates the issue tracker**: At least five active issues describe excessive consumption — from polling busy-waits ([#36396](https://github.com/openai/codex/issues/36396)), idle wait/status re-entry ([#35259](https://github.com/openai/codex/issues/35259)), large image resends ([#28316](https://github.com/openai/codex/issues/28316)), and possible accounting errors ([#36353](https://github.com/openai/codex/issues/36353)). The cumulative signal: users feel credits are consumed wastefully by the client itself.
- **Windows-specific regressions are recurring**: WSL Git detection broke ([#35119](https://github.com/openai/codex/issues/35119)), GPU process crashes from vk_swiftshader ([#34133](https://github.com/openai/codex/issues/34133)), chrome plugin updates leave stale state ([#32706](https://github.com/openai/codex/issues/32706)), and startup crashes on "Invalid weekday string: MON" ([#36225](https://github.com/openai/codex/issues/36225)).
- **Resource leaks remain unresolved**: MCP server processes never cleaned up ([#30408](https://github.com/openai/codex/issues/30408)) and runaway ffmpeg children consuming 900% CPU ([#36345](https://github.com/openai/codex/issues/36345)) indicate systemic process-lifecycle issues.
- **macOS extension instability**: Codex Diff crashes for Apple Silicon users ([#35058](https://github.com/openai/codex/issues/35058)) and Computer Use fails to load `@oai/sky` due to empty `nodeRepl.env` ([#34471](https://github.com/openai/codex/issues/34471)).
- **Memory/context bloat**: Repeated `base64` image resends ([#28316](https://github.com/openai/codex/issues/28316)) and unbounded session/turn state ([#25779](https://github.com/openai/codex/issues/25779)) frustrate long-running workflows with slowdowns and lost control.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-01

## Today's Highlights

Two critical fixes shipped today: a patch preventing retry hangs when capacity limits are exhausted, and improved error messaging that surfaces `InvalidStreamError` details to guide users on empty responses. A notable regression in v0.53.0 involving `thoughtSignature` stripping (causing 400 errors on parallel tool calls) has two concurrent PRs addressing it, signaling user impact. The ongoing theme remains subagent reliability, with several high-priority issues around agent hangs and false success reporting still unresolved.

---

## Releases

**v0.53.1** (stable, patched)
- Cherry-pick of f47d6c6 (capacity exhaustion fix) to stable release line, with manual conflict resolution noted.
- **Full Changelog**: https://github.com/google-gemini/gemini-cli/compare/v0.53.0...v0.53.1

**v0.54.0-preview.1** (preview, patched)
- Same capacity exhaustion fix backported to preview line.
- **Full Changelog**: https://github.com/google-gemini/gemini-cli/pull/28609

**v0.55.0-nightly.20260801.gf47d6c6f7**
- `fix(core)`: classify capacity exhaustion as terminal to prevent retry hangs ([#28599](https://github.com/google-gemini/gemini-cli/pull/28599))
- `fix(core,cli)`: propagate `InvalidStreamError` details to UI for specific empty response guidance ([#28566](https://github.com/google-gemini/gemini-cli/pull/28566))

---

## Hot Issues

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery after MAX_TURNS falsely reports GOAL success** 
   `codebase_investigator` reports `status: "success"` even when it hit its turn limit before doing any work. This hides interruptions and undermines trust in agent results. 12 comments, 2 👍. High priority (P1).

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever** 
   Simple operations like folder creation hang indefinitely when deferred to the generalist agent. Users report waiting up to an hour before cancelling. Workaround: explicitly instructing the model to avoid subagents. 8 comments, 8 👍 — highest community engagement.

3. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command stuck with "Waiting input" after completion** 
   After executing simple, non-interactive CLI commands, the shell state remains "active" with "Awaiting user input" indefinitely. P1 with 3 👍.

4. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini doesn't use skills and sub-agents enough** 
   Anecdotal but recurring: the model ignores custom skills/subagents unless explicitly instructed, even for highly relevant tasks. This undermines the value proposition of custom agent configuration.

5. **[#28566](https://github.com/google-gemini/gemini-cli/pull/28566) — InvalidStreamError propagation** (in releases today)
   The fix itself generated discussion — community eager for actionable guidance on empty responses (e.g., `/compress` recommendation).

6. **[#22093](https://github.com/google-gemini/gemini-cli/issues/22093) — Subagents running without permission since v0.33.0** 
   Users with agents disabled report subagents (like generalist) being invoked anyway. Config expectations violated — a trust issue.

7. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely** 
   Sessions deemed low-signal are never marked processed, so they resurface on every run, wasting tokens and time.

8. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error with >128 tools** 
   Scale ceiling: too many MCP/tools trigger hard API errors instead of intelligent tool selection. Growing concern as MCP ecosystems expand.

9. **[#21763](https://github.com/google-gemini/gemini-cli/issues/21763) — `/bug` report lacks subagent context** 
   Diagnostics blind spot: bug reports only capture main-session context, making subagent failures hard to debug.

10. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland** 
    Environment-specific but recurring: browser agent crashes in Wayland sessions, limiting Linux desktop usage.

---

## Key PR Progress

1. **[#28608](https://github.com/google-gemini/gemini-cli/pull/28608) — Fall back to stable models when preview 404s** 
   Fixes a startup crash when a Gemini API key lacks preview model access — the fallback chain now handles 404s gracefully. P2, area/agent.

2. **[#28607](https://github.com/google-gemini/gemini-cli/pull/28607) — Preserve `thoughtSignature` when stripping thought parts** 
   Direct fix for the v0.53.0 `API Error 400: Function call is missing a thought_signature` regression. P1, area/agent, size/m.

3. **[#28586](https://github.com/google-gemini/gemini-cli/pull/28586) — Preserve `thoughtSignature` in functionCall parts (alternate fix)** 
   Competing fix for the same 400 error regression. #28607 is a follow-up to this; both being evaluated. P2, size/m.

4. **[#28481](https://github.com/google-gemini/gemini-cli/pull/28481) — Refresh MCP OAuth tokens with stored client ID** 
   Fixes OAuth refresh failures that deleted stored credentials, forcing re-auth every session. P1, area/security, size/m.

5. **[#28551](https://github.com/google-gemini/gemini-cli/pull/28551) — Fall back to embedded macOS seatbelt profiles** 
   Resolves startup crash in sandbox mode on macOS/gMac when `.sb` profiles are missing. Size/l — significant surface area.

6. **[#28557](https://github.com/google-gemini/gemini-cli/pull/28557) — Fix SSRF in web-fetch.ts via async DNS resolution** 
   Security hardening: replaces sync `isPrivateIp()` with async variant to catch hostnames resolving to internal IPs (e.g., `169.254.169.254`). P1, area/security.

7. **[#28519](https://github.com/google-gemini/gemini-cli/pull/28519) — Prevent infinite auth loop** 
   Fixes #28430 by awaiting `oauth_creds.json` write and forcing consent. P1, area/core, size/s.

8. **[#28566](https://github.com/google-gemini/gemini-cli/pull/28566) — Propagate `InvalidStreamError` details to UI** (merged; in v0.53.1/v0.54.0-preview.1)
   Users now get actionable advice (e.g., `/compress`) when hitting empty responses. Multi-size PR (m, l, xl) — broad changeset.

9. **[#28606](https://github.com/google-gemini/gemini-cli/pull/28606) — "Setapart" (placeholder)** 
   Skeleton PR with no description content. Likely auto-created or abandoned; watch for updates.

10. **[#28609 / #28610](https://github.com/google-gemini/gemini-cli/pull/28610) — Cherry-picks of capacity exhaustion fix to release lines** 
    Robot-managed patch backports to stable (v0.53.1) and preview (v0.54.0-preview.1) lines. #28610 hit merge conflicts — flagged for manual resolution.

---

## Feature Request Trends

- **Agent self-awareness & control**: Users want Gemini to better understand its own capabilities (flags, hotkeys, subagent selection) and to respect configuration (disabled agents, custom skills). Issues #21432, #21968, #22093.
- **AST-aware tooling**: EPIC #22745 and follow-up #22746 push for AST-aware file reads/search/mapping to reduce token noise and improve code navigation precision.
- **Subagent trajectory visibility**: Request for `/chat share` to expose subagent trajectories for easier review/eval (#22598) and `/bug` reports to include subagent context (#21763).
- **Auto Memory robustness**: Multiple issues (#26522, #26523, #26525, #26516) request deterministic redaction, quarantine of invalid patches, and avoiding indefinite retries.
- **Browser agent resilience**: Automatic session takeover, lock recovery (#22232), and proper `settings.json` override handling (#22267).

---

## Developer Pain Points

- **Silent false success**: The recurring pain is agents reporting `GOAL` success when they actually hit limits or failed (e.g., #22323) — erodes trust in automation.
- **Hangs with no diagnostics**: Generalist agent hangs (#21409), shell "Waiting input" (#25166), and capacity retry loops — users wait minutes to hours with no actionable output.
- **Config broken by updates**: Subagents running despite being disabled (#22093) and browser agent ignoring `settings.json` (#22267) — surprises after upgrades.
- **Regression churn in v0.53.0**: `thoughtSignature` stripping (#28607, #28586) is the second notable regression in a single release — users express frustration with rapid-release stability.
- **Threshold ceilings**: 400 errors with >128 tools (#24246) — scaling pain for power users with heavy MCP setups.
- **Diagnostics gaps**: Bug reports fail to capture subagent context (#21763) — makes root-causing agent failures nearly impossible without manual digging.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-01

## Today's Highlights
Two significant regressions were closed this week: a blocking bug in plan mode that prevented shell command execution (#4188) and a crash triggered by JavaScript-to-Rust type conversion failures after upgrading to v1.0.76 (#4305). A growing concern is the regression in large session resume performance introduced in v1.0.74, which causes severe memory spikes and CPU grinding (#4251). The new v1.0.78-0 release adds permission approval mode switching and improves sandboxed build reliability by enabling toolchain caches by default.

## Releases
**v1.0.78-0** (released 2026-07-31)
- **Added**: New `/permissions` command to switch between approval modes.
- **Added**: ACP (Agent Client Protocol) mode now supports closing sessions via the `closeSession` request.
- **Improved**: New sandbox setting `allowDevToolCaches` (enabled by default) grants sandboxed builds access to toolchain caches, registries, and installs, improving build reliability. This replaces the earlier `allowDevToolRegistry` setting.

## Hot Issues
1. **[#4188 — Regression: Plan mode blocks shell commands](https://github.com/github/copilot-cli/issues/4188)** — *Closed* (7 comments, 3 👍). Plan mode now blocks shell commands like `gh`, which were previously used to enrich plans. Community flagged this as a regression, and it has been closed. High impact for workflow automation.
2. **[#4305 — JavaScript 'Undefined' to Rust 'String' conversion failure](https://github.com/github/copilot-cli/issues/4305)** — *Closed* (4 comments, 4 👍). Users upgrading to v1.0.76 immediately hit persistent conversion errors on any command. Closed after a fix; high visibility due to rapid onset post-upgrade.
3. **[#4251 — Large session resume OOMs in v1.0.74 (regression)](https://github.com/github/copilot-cli/issues/4251)** — *Open* (1 comment, 1 👍). Resuming long-lived sessions now consumes 3–4× memory and grinds one CPU core for ~70 minutes. Isolated via A/B testing to v1.0.74. Critical for daily-driver users with persistent sessions.
4. **[#4078 — Scheduled prompts kill the existing prompt queue](https://github.com/github/copilot-cli/issues/4078)** — *Open* (4 comments). When `/every` or `/after` triggers, the current queue is abandoned—the scheduled prompt runs but the next queued item never pops. Disrupts automation workflows.
5. **[#4161 — task_complete tool unavailable after switching back to autopilot mode](https://github.com/github/copilot-cli/issues/4161)** — *Closed* (4 comments, 4 👍). A reported regression of an older issue (#1523), where `task_complete` was filtered out after mode switching. Closed; community remains vigilant about this recurring pattern.
6. **[#3183 — SDK: orphan tool_use causes 400 errors after resume](https://github.com/github/copilot-cli/issues/3183)** — *Closed* (4 comments). SDK-level bug where orphaned `tool_use` blocks without `tool_result` blocks break session resume. Closed after investigation; important for SDK integrators.
7. **[#3909 — Enterprise feature request: org-managed settings for local CLI](https://github.com/github/copilot-cli/issues/3909)** — *Open* (4 comments). Org admins cannot centrally push configuration or environment variables to local CLI installs—only cloud-hosted agents. High demand from enterprise teams.
8. **[#1352 — sessionStart hook stdout silently discarded](https://github.com/github/copilot-cli/issues/1352)** — *Open* (3 comments, 3 👍). Hook output never renders in the terminal, preventing use cases like displaying reminders or environment banners at session start.
9. **[#2109 — ACP: support ask_user / ask_question style extension method](https://github.com/github/copilot-cli/issues/2109)** — *Open* (2 comments, 6 👍). Strong demand for structured user-questioning in ACP. Currently only `session/request_permission` exists; community wants richer interactive extensions.
10. **[#4311 — Transcript blank lines until width change (rendering bug)](https://github.com/github/copilot-cli/issues/4311)** — *Open* (1 comment). Interactive transcript blanks out until terminal resize or new message; `/resume` does not recover. Likely related to a measured-line cache invalidation bug.

## Key PR Progress
Note: Only 2 PRs were active in the last 24h; both are open and appear to be low-quality or test PRs. The broader community-reported issues above are the primary signal this week.
1. **[#3163 — ViewSonic monitor (testing/CI)](https://github.com/github/copilot-cli/pull/3163)** — *Open*. Referenced in PR body as related to issues #2591, #3561, #3559. No substantive feature changes; appears to be an infrastructure-only change.
2. **[#4316 — Create devcontainer.json](https://github.com/github/copilot-cli/pull/4316)** — *Open*. Adds a devcontainer configuration; no description provided. Likely a contributor convenience PR, not a feature change.

## Feature Request Trends
- **Enterprise/Org Administration**: Strong push for centrally managed configuration, environment variables, and settings for local CLI installs (#3909). Enterprise teams need policy enforcement beyond cloud-hosted agents.
- **ACP Extension Depth**: Community requests more interactive capabilities in the Agent Client Protocol—specifically structured user-questioning (`ask_user`) and token/context usage reporting (#2109, #4174). Integrators want parity with interactive mode.
- **Terminal UX**: Requests for session history scrolling (#4313) and pinned session sections in desktop UI (#4321) suggest growing adoption as a primary terminal tool.
- **External Model/Tool Support**: Interest in supporting non-GitHub models (e.g., DeepSeek) and richer tool semantics (e.g., custom agent MCP tools two levels deep—#4320) indicates users are pushing boundaries beyond default configurations.

## Developer Pain Points
- **Regression Frequency**: Multiple week-over-week regressions in plan mode (#4188), autopilot tools (#4161), and session resume performance (#4251, #3183). The community is increasingly wary of updates breaking existing workflows.
- **Resume Reliability**: Large session resume is fragile—both performance degradation (#4251) and hard failures when `events.jsonl` exceeds V8's max string length (#4325) leave users with unloadable sessions.
- **Configuration Friction**: Strict `.mcp.json` JSON parsing rejects comments (#4323), and MCP interactive wizard lacks help for environment variable format (#1478). Small config hurdles that add up.
- **Sandbox and Permission Confusion**: Issues around sandbox limitations (ReFS on Windows—#3712) and permission mode switching (#4188) suggest the security model is still maturing and not yet intuitive.
- **Version Pinning Gap**: Reports that "installing a specific version always installs the latest" (#4317) undermine trust in the installer's reliability, especially for users who need to pin versions to avoid regressions.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-01

## Today's Highlights

No new releases landed this week, but the community remains highly engaged on two long-running feature fronts: **Remote Control** (#1282, 23 👍) and a **Persistent Memory System** (#1283) — both proposed by the same author in February and still drawing active discussion. The maintainers appear to be prioritizing stability, with a fresh PR (#2572) addressing a critical double-encoded JSON bug in tool-call arguments that has been causing Pydantic validation failures across providers.

---

## Releases

No new releases in the last 24 hours. Previous stable version remains **v1.46.0** (referenced in issue reports).

---

## Hot Issues

### 1. [#1282 — Feature Request: Remote Control](https://github.com/MoonshotAI/kimi-cli/issues/1282)
**Author:** CatKang | **State:** Open | **Comments:** 9 | **👍:** 23  
A heavily upvoted request to continue local CLI sessions from any device (phone, tablet, browser). This addresses a core friction point for developers who need workflow continuity away from their desk. The high 👍 count signals strong demand for a web-based companion or session-mirroring layer.

### 2. [#1283 — Feature Request: Memory System](https://github.com/MoonshotAI/kimi-cli/issues/1283)
**Author:** CatKang | **State:** Open | **Comments:** 8 | **👍:** 0  
Proposes both automatic (AI-managed) and manual (user-defined) persistent memory across sessions — project patterns, preferences, and context that survive restarts. Pairing with #1282, this forms a vision for a more autonomous, personalized assistant. Low 👍 but active discussion suggests niche-but-passionate interest.

### 3. [#2422 — [bug] Scrolling jumps to bottom after conversation completes](https://github.com/MoonshotAI/kimi-cli/issues/2422)
**Author:** venus0707 | **State:** Open | **Comments:** 2 | **👍:** 1  
A terminal UX annoyance: after a conversation finishes, scrolling up to review output forcefully snaps back to the bottom. Small but frequently encountered friction that degrades long-session usability. The user reports on Linux with kimi2.6 and v1.46.0.

### 4. [#796 — [closed] "message at position 1 with role" Pydantic error](https://github.com/MoonshotAI/kimi-cli/issues/796)
**Author:** bravery | **State:** Closed | **Comments:** 1 | **👍:** 0  
An old macOS-specific LLM provider error (HTTP 400) with `kimi-for-coding` model. Closed, but the underlying class of provider-format incompatibility remains relevant — and is precisely what new PR #2572 attempts to fix at the JSON-unwrapping level.

---

## Key PR Progress

### 5. [#2572 — fix(kosong): recursively unwrap double-encoded JSON in tool-call arguments](https://github.com/MoonshotAI/kimi-cli/pull/2572)
**Author:** aalhadxx | **State:** Open | **Created:** 2026-07-31  
**Impact:** High. Fixes Pydantic validation errors for array/object params (e.g., `SetTodoList`, `ExitPlanMode`, `StrReplaceFile`) when providers like Moonshot API double-encode nested values as JSON strings. This is an enabling fix for multi-provider reliability and directly addresses a class of "provider incompatibility" bugs.

---

## Feature Request Trends

Distilling from current open requests, three dominant directions emerge:

1. **Continuous / Remote Access** — The ability to detach, roam, and resume sessions from other devices (see #1282).
2. **Persistent Memory & Context** — Cross-session recall of project conventions, user preferences, and AI-maintained notes (#1283).
3. **Terminal UX Polish** — Small but high-frequency quality-of-life fixes: scroll control after completion (#2422), output review ergonomics, and stable rendering across terminal emulators.

The community is clearly pushing Kimi Code CLI beyond a stateless REPL toward a **persistent, context-aware coding companion** that lives across devices.

---

## Developer Pain Points

- **Provider Compatibility Fragility:** Pydantic validation failures due to provider-specific JSON encoding (see #796, #2572) remain the most technical recurring frustration — multi-provider support is valued but brittle.
- **Session Continuity Gaps:** Starting a session on one machine and being unable to continue it elsewhere is a visible blocker for remote/hybrid workflows (#1282).
- **Context Amnesia:** Re-explaining project conventions and settings to the CLI on every new session is a repeated complaint echoed in #1283’s discussion.
- **Terminal Interaction Nuances:** Post-conversation scroll behavior (#2422) and similar terminal-related UX issues surface regularly, indicating that CLI interaction quality is carefully scrutinized by this audience.

---

*Digest compiled 2026-08-01 from public GitHub data for MoonshotAI/kimi-cli.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-01

## 1. Today's Highlights

A wave of **upstream provider auth failures** (401 errors) is impacting paid OpenCode Go/Zen subscribers, with multiple open threads and no official fix yet — this is the community's top concern. Meanwhile, the team is actively **cleaning up dead code** across the TUI and CLI via a rapid series of contributor PRs, and **DeepSeek V4 Flash's formal release** has the community asking whether the new checkpoint is already available on OpenCode's managed services. Privacy policy changes around Go's data-retention wording have also sparked a notable backlash.

---

## 2. Releases

**No new releases in the last 24 hours.**

---

## 3. Hot Issues

1. **[#38257 — OpenCode Go: 401 Request blocked by upstream provider](https://github.com/anomalyco/opencode/issues/38257)** — *42 comments*  
   A server-side block on `chat/completions` for all Go subscription models while `/v1/models` still works. The 11 👍 reflect widespread impact; users report the issue started abruptly on July 22 and persists. This is a **critical availability bug** for paying customers.

2. **[#4140 — Black screen when using >1.0.46](https://github.com/anomalyco/opencode/issues/4140)** — *37 comments*  
   A long-running TUI rendering regression (opened Nov 2025) that forces users to pin old versions. The issue was closed, but user activity continues into this week, suggesting the fix may not have fully satisfied the community.

3. **[#39823 — DeepSeek V4 Flash formal version (0731) live on Go/Zen?](https://github.com/anomalyco/opencode/issues/39823)** — *22 comments*  
   With **20 👍**, this is the hottest topic today. The community wants confirmation and rollout details for DeepSeek-V4-Flash-0731 (retrained checkpoint with better agent benchmarks) on OpenCode's managed offerings.

4. **[#39875 — Revert silent removal of Go privacy wording and provider attribution](https://github.com/anomalyco/opencode/issues/39875)** — *4 comments, 20 👍*  
   A coordinated feature request citing four related issues (#39860, #39857, #24649, #14281). Users demand explicit telemetry/retention policies and transparency about which upstream providers serve their traffic — a **trust issue** gaining rapid traction.

5. **[#24316 — Progress halts with qwen 3.6 35b-a3b on naked tool call](https://github.com/anomalyco/opencode/issues/24316)** — *20 comments*  
   A tricky integration bug where the model emits a raw `<tool_call>` in the console and freezes. The three-way blame debate (llama.cpp vs. qwen vs. OpenCode) continues, but local-LLM users are clearly hitting this daily.

6. **[#39827 — [Zen] AuthError on all models, account recreated](https://github.com/anomalyco/opencode/issues/39827)** — *2 comments*  
   A companion to the Go 401 issue: **all Zen models** (paid and free) return `Request blocked by upstream provider`, while direct provider keys work. Suggests the upstream block is account/route-wide, not model-specific.

7. **[#17505 — session/update notifications arrive after end_turn](https://github.com/anomalyco/opencode/issues/17505)** — *15 comments, 10 👍*  
   A protocol-level bug for ACP integration (Fabriqa). Clients finalize turns with empty content because `session/update` events arrive too late. Important for the **ecosystem/agent-interop** direction OpenCode is pushing.

8. **[#38801 — "exiting loop" message](https://github.com/anomalyco/opencode/issues/38801)** — *19 comments*  
   A recurring, cryptic runtime message that halts sessions. The report captures broader frustration with TUI stability: *"I put it away for another day"* is a common sentiment among affected users.

9. **[#39861 — Removal of zero-data-retention policy](https://github.com/anomalyco/opencode/issues/39861)** — *4 comments, 13 👍*  
   Directly tied to #39875: the zero-retention promise was silently removed from Go docs. Users are asking for an **official policy statement** rather than incidental doc edits. This is a governance red flag for enterprise adoption.

10. **[#23595 — <system-reminder> moves around, breaking cache](https://github.com/anomalyco/opencode/issues/23595)** — *4 comments, 11 👍*  
    Local-LLM users report that prompt cache hit rates collapse because the system reminder is relocated between turns. High impact for **llama.cpp/vLLM power users** who rely on prompt caching to keep costs down.

---

## 4. Key PR Progress

1. **[#39982 — Concise error output for failed shell commands](https://github.com/anomalyco/opencode/pull/39982)** *(OPEN)*  
   Part 3 of #39771: returns a 50-line/8-KB tail on non-zero exits instead of the full output. A welcome UX improvement — long error dumps currently flood the TUI.

2. **[#39981 — Watch newly created plugin directory](https://github.com/anomalyco/opencode/pull/39981)** *(OPEN)*  
   Fixes silent failure when `.opencode/plugins/tui/` is created after startup. The TUI previously stopped watching the missing path without any signal — a real plugin-dev workflow breaker.

3. **[#39942 — Persist tab reorder once per drag](https://github.com/anomalyco/opencode/pull/39942)** *(CLOSED)*  
   Reduces redundant `flock → read → write` cycles during tab drags. Previously, each slot crossing triggered an atomic write to `tabs.json`; now the gesture persists once. Better multi-client tab consistency.

4. **[#39941 — Harden session tab state hygiene](https://github.com/anomalyco/opencode/pull/39941)** *(CLOSED)*  
   Three fixes: surfaces silent persistence failures (`.catch(() => {})` removed), tightens `closeSession` sequencing, and prevents tabs mysteriously resetting on launch.

5. **[#39940 — Ignore hidden tab close hitbox](https://github.com/anomalyco/opencode/pull/39940)** *(CLOSED)*  
   The `×` close mark only renders on hover, but its `onMouseUp` was always active — causing **invisible accidental tab closes** on terminals without motion tracking. Nice catch.

6. **[#39980 — Test: wait for mini prompt readiness](https://github.com/anomalyco/opencode/pull/39980)** *(CLOSED)*  
   Removes a flaky-test race condition by exposing prompt-listener readiness and waiting for explicit model/prompt/turn-start signals. Improves TUI test reliability.

7. **[#5657 — Toggle transparent background](https://github.com/anomalyco/opencode/pull/5657)** *(OPEN)*  
   A tri-state transparency policy (`auto | on | off`) for the TUI theme, persisted via `theme_transparent`, with a new command palette entry. Blends well with terminal aesthetic customization requests.

8. **[#39964 — Remove unused duration formatter](https://github.com/anomalyco/opencode/pull/39964)** *(CLOSED)*  
   Part of a **broad dead-code cleanup wave** (see #39952–#39963): removes unused utilities, tests, and dependencies to reduce bundle size and maintenance surface. Maintainer @kitlangton is actively driving this.

9. **[#39955 — Remove placeholder LSP panel](https://github.com/anomalyco/opencode/pull/39955)** *(CLOSED)*  
   Deletes the built-in sidebar LSP panel that only reported "unavailable" — a misleading no-op that confused users expecting LSP support.

10. **[#39953 — Remove prompt re-export barrels](https://github.com/anomalyco/opencode/pull/39953)** *(CLOSED)*  
    Deletes transitional re-export barrels under `component/prompt`, redirecting consumers to canonical modules. Simplifies the TUI's internal API surface ahead of future refactors.

---

## 5. Feature Request Trends

- **Marketplace / plugin registry is the top unmet need** — Issue #28696 ("Plugin/Agent/Skills marketplace," 23 👍) remains the community's most-voted open feature. Users want a unified discovery, distribution, and versioning system rather than manual `.opencode/plugins` directory management.
- **Text selection in the TUI** — Issue #927 (29 👍, long closed but still referenced) reflects persistent demand for mouse-selectable text in the terminal UI, a baseline ergonomics feature many users consider missing.
- **Privacy & transparency controls** — A new cluster (#39861, #39875) demands explicit telemetry settings and opt-in data retention rather than silent policy changes. Expect this to grow as OpenCode pushes managed services.
- **Session/prompt management** — Issue #24017 asks for saved prompts, threads, topics, and bookmarks. Combined with #39840 (cross-project session navigation), users want a more robust session system with navigation and organization.
- **Richer desktop/VSCode integration** — #39936 (VSCode notifications), #39944 (collapse tool panels in desktop app) — the desktop experience lags the TUI in configurability and polish.

---

## 6. Developer Pain Points

- **Managed service reliability (Go/Zen)** is the **most urgent issue today**: upstream 401 blocks (#38257, #39827), billing anomalies on `qwen3.7-max` (#36399), and model-specific stream degradation (#39881). Paying users are experiencing multi-day outages with little official communication, eroding trust.
- **Local LLM integration remains fragile**: repeated reports of prompt cache busting (#23595) and tool-call parsing failures (#24316) suggest OpenCode's request construction is not yet stable across llama.cpp/vLLM/Ollama backends.
- **Stale, cryptic errors are common**: "exiting loop" (#38801), SQLite `session_message.seq` constraint crashes (#39165), and silent persistence failures (#39941) hint at insufficient error surface — failures are either silent or opaque.
- **TUI stability has a long tail**: black-screen regressions (#4140, #10221, #16185) and rendering glitches (#38773) keep recurring across versions. The maintainers' current cleanup wave is healthy, but users have been burned by regressions since late 2025.
- **ACP/protocol timing bugs** (#17505) and mid-session message drops (#32719) are blocking serious ecosystem integrations — these are foundational issues that need hardening before OpenCode can be a reliable agent platform.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-01

## Today's Highlights
A substantial infrastructure push around session persistence and server architecture landed this week, with a dozen PRs from christianklotz converging on a durable, concurrent-safe session backend. A critical fix targeting baseline x64 CPU compatibility (SIGILL crash on pre-Haswell) is now in review, alongside a Wayland clipboard fix that closes a long-standing paste-breaking bug. The most active issue this cycle remains Pi login hangs in WSL during GitHub Copilot device auth — a 19-comment investigation with no resolution yet.

## Hot Issues

1. **[#6187 — Pi login hangs in WSL after browser-based GitHub Copilot device authorization](https://github.com/earendil-works/pi/issues/6187)**  
   The longest-running unresolved issue this cycle (19 comments). Device registration succeeds in the browser, but the WSL client never detects completion and hangs indefinitely. High visibility with no maintainer-confirmed fix yet — a severe onboarding blocker for WSL users.

2. **[#6879 — auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)**  
   5 👍, community-backed report: a session on gpt-5.6-sol ran a single agentic turn over 2 hours, blowing past the compaction threshold all the way to API rejection at 373k tokens. Users want compaction checks after *every* agent turn, not just at boundaries.

3. **[#6665 — TUI pins a full core while streaming: uncached Intl.Segmenter + per-chunk Markdown rebuild](https://github.com/earendil-works/pi/issues/6665)**  
   In-progress performance bug: long sessions cause 100% CPU on one core during streaming. Root cause identified — uncached grapheme segmentation with ICU BreakIterator plus per-chunk Markdown re-render. Affects the core TUI on `pi -ne`, so impact is wide.

4. **[#7020 — Sometimes Pi doesn't continue after compaction](https://github.com/earendil-works/pi/issues/7020)**  
   2 👍, in-progress. Long-running "coordinator" sessions hit warts in compaction where the session never resumes after the operation completes. Compaction reliability is clearly a recurring theme across multiple issues this week.

5. **[#7161 — anthropic-messages never sends x-client-request-id, unlike all OpenAI paths](https://github.com/earendil-works/pi/issues/7161)**  
   Gateway operators can't maintain session affinity for Anthropic conversations because the request-id header is missing. Breaks round-robin/load-balancing setups with multiple Claude accounts — an integration gap, not just cosmetic.

6. **[#7053 — Parallel tool batches lose already-completed tool results when one sibling stalls](https://github.com/earendil-works/pi/issues/7053)**  
   Follow-up to #3503: the UI decoupling fix landed, but persisted toolResult messages still wait for the entire batch via `Promise.all`. A stalled sibling orphanes completed tool calls, producing "No result provided" errors — wasted tokens and broken agent momentum.

7. **[#7149 — Standalone linux-x64 binary SIGILL on pre-Haswell CPUs (BMI2)](https://github.com/earendil-works/pi/issues/7149)**  
   Binary ships with BMI2 instructions, crashing on Sandy Bridge-era CPUs (`shlx` in gdb). npm package works fine — only the standalone binary is affected. A compatibility PR (#7390) is now in review.

8. **[#7290 — `--mode json` emits O(n²) stdout for a single tool call; large writes OOM the agent](https://github.com/earendil-works/pi/issues/7290)**  
   Every `message_update` carries the full cumulative assistant message — a 64 KB HTML write burned 17 minutes and produced nothing. Critical for batch/server workloads using JSON mode.

9. **[#7253 — /compact triggers compact twice when context window reached 90%](https://github.com/earendil-works/pi/issues/7253)**  
   Manual `/compact` at high context triggers auto-compaction concurrently, then a third runaway attempt that requires Esc to abort. The error message ("Compaction failed: Already running") confirms state-machine confusion.

10. **[#6996 — Gemini 3.x models fail during tool use due to missing thought_signature in history](https://github.com/earendil-works/pi/issues/6996)**  
    Gemini 3.5/3.6 flash models error when a tool result is submitted back, because the conversation history is missing the expected `thought_signature` field. Production agents on Gemini are blocked on multi-turn tool loops.

## Key PR Progress

1. **[#7381 — Make model refresh state consistent](https://github.com/earendil-works/pi/pull/7381)** *(OPEN)*  
   Consolidates model-catalog refresh across ownership boundaries (provider refresh vs `/model` vs login/logout vs extension registration). Addresses a class of race conditions in provider state.

2. **[#7390 — Target baseline x64 CPUs](https://github.com/earendil-works/pi/pull/7390)** *(OPEN)*  
   Direct fix for #7149: strips BMI2 from build targets so binaries run on pre-Haswell hardware. One-line scope, high user value.

3. **[#7387 — Read clipboard text on Wayland](https://github.com/earendil-works/pi/pull/7387)** *(CLOSED)*  
   Adds `wl-paste` fallback before X11 clipboard reads, with regression coverage for empty/Wayland clipboard states and fallback behavior. Closes #7248 — Ctrl+V now works on Wayland sessions.

4. **[#7394 — Make JSON streaming output linear](https://github.com/earendil-works/pi/pull/7394)** *(OPEN)*  
   Fixes #7290: emits delta-only `message_update` records in JSON/RPC mode, preserves cumulative snapshots internally, adds stdout backpressure. Documents the breaking wire-protocol migration — necessary cost for fixing O(n²) blowups.

5. **[#7396 — Add server session backend](https://github.com/earendil-works/pi/pull/7396)** *(OPEN)*  
   Durable JSONL-backed server backend with exclusive cross-process locking and crash recovery. Part of the server-mode push; makes remote sessions production-viable.

6. **[#7404 — Add Baseten provider](https://github.com/earendil-works/pi/pull/7404)** *(CLOSED)*  
   New built-in API-key provider (OpenAI-compatible) using a single `openai-completions` endpoint. Mirrors the Together AI integration pattern — low-risk provider expansion.

7. **[#7409 — Add remote session client coordination](https://github.com/earendil-works/pi/pull/7409)** *(CLOSED)*  
   Adds `PiClient` connection ownership, idempotent disposal, shared/exclusive session leases, and idempotent server detach. Enables concurrent multi-client access to one session without corruption.

8. **[#7386 — Add composable protocol server](https://github.com/earendil-works/pi/pull/7386)** *(CLOSED)*  
   Transport-independent `PiServer` with authenticated framed-CBOR protocol, Unix listener building block, and testing conformance helpers. The architectural foundation for remote/server workflows.

9. **[#7389 — Add native prompt API for extensions](https://github.com/earendil-works/pi/pull/7389)** *(CLOSED)*  
   Exposes `pi.prompt()` to extensions, routing through native command/skill/prompt-template handling with image and streaming preservation. Fixes #7277 where `sendUserMessage("/reload-runtime")` silently did nothing.

10. **[#6216 — Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216)** *(OPEN)*  
    Adds Bedrock Mantle's OpenAI Responses API support via OpenAI's Bedrock provider. Supersedes an earlier attempt — enterprise AWS users get a first-party path.

## Feature Request Trends
- **Server/remote architecture is the dominant direction**: The christianklotz PR cluster (#7386, #7396, #7408, #7409, #7411) builds toward a composable protocol server with durable session backends, explicit client leases, and protocol conformance testing. This reads as preparation for a first-class headless/server mode.
- **Extending the extension API**: Multiple asks converge on richer extension capabilities — native `pi.prompt()`, reliable command triggering post-agent-settle (#7277), and documented custom provider parity (#7267). The extension surface is emerging as a core product priority.
- **Provider breadth by adoption**: Baseten (merged) and Bedrock Mantle (open) follow the established pattern of wrapping OpenAI-compatible endpoints. Kimi K3 on Fireworks (#7199) was closed by regenerating from models.dev — the generator path continues to suffice for named models.
- **Context/compaction reliability**: Beyond the specific bugs, the cluster of compaction, context-limit, and JSON-output issues suggests users are running longer, more complex agentic sessions than the compaction heuristics were originally designed for.

## Developer Pain Points
- **Context window management is the #1 pain**: Compaction misfires (twice, not-at-all, or blocking resumption), O(n²) JSON blowups, and missing per-turn checks. For long-running "coordinator" sessions and multi-hour agentic turns, the current heuristics are dangerously close to the edge.
- **Compatibility regressions erode trust in binaries**: SIGILL on older CPUs and Wayland clipboard failures both shipped in release binaries with no test coverage. The community reaction is swift (repros, gdb traces), but these are category errors that should be caught pre-release.
- **Parallel tool execution has a data-integrity gap**: #7053 shows completed tool results can be lost when a sibling stalls. For agent frameworks, losing an already-executed tool result means wasted API spend and incorrect downstream reasoning — the community is treating this as a correctness bug, not a UI nuance.
- **OAuth flows are fragile in enterprise/WSL contexts**: WSL login hangs (#6187), Copilot GHE.com compaction failures (#7413), and kimi-coding 401s (#7319) all share a pattern — the browser-out-of-band dance is underspecified for non-standard environments. Gateway admins also feel the lack of request-id headers (#7161) as an operational gap.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-01

## Today's Highlights

The Qwen Code team shipped **v0.21.2** with a critical fix for the TUI: SGR mouse escape sequences were leaking into the input buffer, and a new `ui.mouseTracking` setting now restores right-click and URL-click functionality. Meanwhile, the autofix pipeline gained maturity with round-limit constraints (deferring lower-severity suggestions after five rounds) and a new PR to ensure the review runner always uses the latest qwen CLI. The daemon architecture continues to evolve with multiple RFCs and tracking issues around multi-workspace resource bounding, reflecting a strong focus on production-grade server deployments.

---

## Releases

### v0.21.2
- **Autofix round limits**: Autofix now defers lower-severity suggestions after five rounds and posts visible notices when refusing to proceed due to round limits ([#7913](https://github.com/QwenLM/qwen-code/pull/7913), [#8067](https://github.com/QwenLM/qwen-code/pull/8067))
- **Mouse tracking regression fix**: New `ui.mouseTracking` setting (default: `true`) gates SGR mouse tracking; disabling it restores right-click and URL clicks in VP mode, which was broken since 0.21.1 ([#8198](https://github.com/QwenLM/qwen-code/pull/8198))

---

## Hot Issues (Top 10)

1. **[RFC] Support multiple workspaces in one `qwen serve` daemon** ([#6378](https://github.com/QwenLM/qwen-code/issues/6378)) — *31 comments, closed*  
   The most-discussed issue this week. This RFC proposes moving from "1 daemon = 1 workspace × N sessions" to a multi-workspace model. The community is clearly invested in this direction, with follow-up tracking issues (#8051, #8091) suggesting an active implementation effort.

2. **[Tracking] Bound multi-workspace daemon resource usage** ([#8051](https://github.com/QwenLM/qwen-code/issues/8051)) — *9 comments*  
   Companion to #6378. Identifies that count-only limits don't bound bytes held by request bodies, WebSocket assembly, and other memory paths. The community is pushing for production-ready resource management.

3. **Minified React error #185 in Cherry Studio integration** ([#5199](https://github.com/QwenLM/qwen-code/issues/5199)) — *9 comments*  
   Open for ~6 weeks with a `need-information` status. A Windows user hitting a React crash in the Cherry Studio global install of `@qwen-code/qwen`. Still unresolved, indicating a potentially tricky integration issue.

4. **Deferred tool discovery invalidates prompt cache prefixes** ([#6721](https://github.com/QwenLM/qwen-code/issues/6721)) — *7 comments*  
   Performance issue where `tool_search`-discovered tools call `setTools()`, breaking prompt cache prefixes. Important for cost and latency optimization in long sessions.

5. **Anthropic 4.6+ assistant-prefill 400 + thinking.display silently defaults to 'omitted'** ([#8039](https://github.com/QwenLM/qwen-code/issues/8039)) — *6 comments, closed*  
   Two confirmed bugs affecting Claude Opus/Sonnet 4.6+ and 5.x families. The assistant-turn "prefill" issue caused 400 errors with no mitigation path. High severity (P1) and now resolved.

6. **Daemon authorises each ACP child 50% of host memory, never divided by child count** ([#8182](https://github.com/QwenLM/qwen-code/issues/8182)) — *3 comments*  
   Serious resource-management bug: `getAcpMemoryArgs()` computes a ceiling once and caches it, so N children each get 50% of host memory. Community is engaged on daemon memory hygiene.

7. **JSON-style tool call arguments leak as plain text when model drops function-calling format** ([#8207](https://github.com/QwenLM/qwen-code/issues/8207)) — *3 comments*  
   In production DataAgent sessions, `qwen3.7-max` occasionally serializes tool args into content instead of structured `tool_call`s. Highlights the model-behavior drift issue in long sessions.

8. **Windows: validated @-file reads lose O_NOFOLLOW protection** ([#8227](https://github.com/QwenLM/qwen-code/issues/8227)) — *3 comments*  
   Follow-up to #7206. On Windows, `O_NOFOLLOW` doesn't exist and dev/ino checks may be vacuous, weakening symlink/TOCTOU protections. Security-relevant for Windows users.

9. **qqbot channel truncates sender openid, LLM cannot @-mention sender** ([#8232](https://github.com/QwenLM/qwen-code/issues/8232)) — *3 comments*  
   `prepareGroupMessage()` truncates sender openid to 8 hex chars + ellipsis, but instructions tell the model to use `<@OPENID>` tags. The LLM cannot produce valid mentions with truncated IDs.

10. **SGR mouse escape sequences leak into input box at startup** ([#8267](https://github.com/QwenLM/qwen-code/issues/8267)) — *2 comments*  
   v0.21.2 startup issue where raw SGR Extended Mouse Mode events are injected as text into the input buffer. Mitigated by the new `ui.mouseTracking` setting, but the default behavior needs fixing.

---

## Key PR Progress (Top 10)

1. **[fix(ci)] Upgrade the review runner's qwen CLI to npm latest per run** ([#8265](https://github.com/QwenLM/qwen-code/pull/8265)) — *autofix/takeover*  
   Addresses stale-review-format issues by ensuring the CI review runner installs the latest qwen CLI per run instead of using a cached 0.20.0.

2. **[fix(web-shell)] Isolate automatic recap by session** ([#8262](https://github.com/QwenLM/qwen-code/pull/8262)) — *autofix/takeover*  
   Prevents a recap requested for one session from being injected into a different session's transcript after a session switch. Records originating session + generation for ownership checks.

3. **[fix(web-shell)] Deduplicate permission options with same display label** ([#8250](https://github.com/QwenLM/qwen-code/pull/8250)) — *review/self-reported*  
   Collapses duplicate "Yes, allow once" buttons in the Web Shell's ToolApproval dialog by deduplicating i18n keys and raw labels.

4. **[feat(web-shell)] Support mutable default mid-turn messages** ([#8229](https://github.com/QwenLM/qwen-code/pull/8229)) — *autofix/takeover*  
   Plain-text messages sent mid-turn enter the running turn by default, with a "Queued..." state until daemon injection is confirmed.

5. **[feat(workflows)] Bubble workflow agent approvals** ([#8240](https://github.com/QwenLM/qwen-code/pull/8240)) — *autofix/takeover*  
   Completes the foreground Dynamic Workflow permission path: Shell/edit/MCP/info requests from workflow agents surface through the parent TUI, ACP host, or stream-json channel.

6. **[feat(serve)] Resolve and report the daemon memory budget** ([#8245](https://github.com/QwenLM/qwen-code/pull/8245)) — *autofix/takeover*  
   The daemon has no notion of its memory limit — no cgroup read, no heap limit, no memory field. This PR adds budget awareness and reporting.

7. **[fix(cli)] Keep model switches session-scoped** ([#6579](https://github.com/QwenLM/qwen-code/pull/6579)) — *autofix/takeover*  
   `/model <id>` and model-picker selections now only update the active session. Persisting as default requires explicit `/model --default`. Prevents accidental cross-session model changes.

8. **[feat(cli)] Adopt Goal v3 in interactive TUI** ([#8005](https://github.com/QwenLM/qwen-code/pull/8005)) — *autofix/takeover*  
   Large feature PR connecting the TUI to the Goal v3 runtime: `/goal` lifecycle commands, persistent lifecycle cards, Goal-aware resume/branch recovery, and a two-lane input queue.

9. **[feat(review)] Test Plan claim check, base-tree A/B harness, per-hunk probes** ([#8215](https://github.com/QwenLM/qwen-code/pull/8215)) — *autofix/takeover*  
   Gives `/review` three hands-on verification capabilities: verifying test-plan claims, A/B testing base trees, and per-hunk probing — borrowing from maintainer verification workflows.

10. **[fix(autofix)] State the primary agent budget and use the step's headroom** ([#8257](https://github.com/QwenLM/qwen-code/pull/8257)) — *autofix/takeover*  
   The autofix primary attempt never stated its own budget, so it took `run-agent.mjs`'s 50-minute default while the wrapping step caps at 80 minutes. Fixes the "AutoFix ran out of time" timeout rounds.

---

## Feature Request Trends

1. **Multi-workspace daemon (high demand)**: RFC #6378 with 31 comments is the clearest signal. Users want a single `qwen serve` daemon to handle multiple workspaces with proper resource bounding. Tracking issues #8051 and #8091 show active work on splitting the delivery into reviewable PRs.

2. **Resource governance for daemon/ACP**: Memory limits per child, heap ceilings, and byte-level bounding are recurring themes — #8182 (ACP child memory), #8245 (daemon memory budget), #8051 (resource bounding). Production users need hard limits, not just count limits.

3. **Web Shell UX maturity**: Multiple PRs (#8250, #8262, #8229) are polishing the Web Shell's approval dialogs, mid-turn messaging, and session isolation. The web experience is becoming a first-class citizen alongside the TUI.

4. **Fork profiles & execution gates**: PR #8148 adds project-level named fork profiles (`ro-research` style) with required tool allowlists — a convenience layer over the execution gate from #8066. Indicates growing interest in sandboxed/research workflows.

5. **Review/verification tooling**: The `wenshao` PR stream (#8215, #8242, #8261, #8257) shows heavy investment in automated review capabilities: test-plan claim checking, A/B harnesses, mined maintainer disciplines, and budget-aware autofix.

---

## Developer Pain Points

1. **Model behavior drift in long sessions**: Multiple issues (#8003, #8207, #6721) report models like `qwen3.7-max` and `qwen3.8-max-preview` occasionally emitting XML-style or JSON-style tool calls as plain text instead of structured `tool_calls` after hundreds of turns. This is a recurring class of production-breaking bug.

2. **Anthropic wire compatibility**: Four separate converter bugs surfaced from `netbrah`: prefill 400s, unsanitized `tool_use.id` charsets, non-guaranteed `tool_result` ordering, and orphaned tool calls being stripped (#8039, #8159, #8160, #8161). Anthropic's 4.6+ and 5.x models present real integration friction.

3. **Memory and resource management on Windows**: Windows-specific issues with file-read protections (#8227), clipboard paste support (#7957), and React crashes in Cherry Studio (#5199) suggest the Windows experience lags behind macOS/Linux.

4. **Flaky E2E tests in CI**: Repeated CI failures — acp-cron timing (#8237, #8076), async tool handler delays (#8256, #8222), subagent delegation (#8244), and duplicate tool_use_id issues — point to test-seam and timing-race problems. The community is actively patching with test seams like `QWEN_CODE_TEST_CRON_FAST`.

5. **TUI input handling regressions**: SGR mouse escape sequence leakage (#8267) on startup is a fresh regression in v0.21.2, highlighting the fragility of terminal input handling in the VP-mode default.

6. **Subagent interaction deadlocks**: Issue #7835 (sub-agent asks user questions but main agent doesn't forward them) remains closed but illustrates a UX gap that recurs with agentic workflows — agents can block indefinitely waiting for input that never reaches them.

---

*Digest generated from GitHub data as of 2026-08-01. For full details, see the [QwenLM/qwen-code repository](https://github.com/QwenLM/qwen-code).*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI / CodeWhale Community Digest — 2026-08-01

## 1. Today's Highlights

The v0.9.3 release train has landed, marking a major milestone: DeepSeek V4 Flash direct responses and a canonicalized tool catalog (PR #4993, 72 commits). The project continues its rebranding transition from `deepseek-tui` to **CodeWhale**, with the legacy npm package officially deprecated. Maintenance is buzzing with 13 dependabot PRs and two significant community-contributed fixes: AltGr key handling on Windows (PR #4977) and actionable File-edit diagnostics (PR #5008). The issue tracker is active with 19 items, headlined by a Chinese-language translation debate and several v0.9.3 enhancement proposals around ACP protocol support, OAuth headless flows, and sandbox path controls.

## 2. Releases

**[v0.9.3](https://github.com/Hmbown/CodeWhale/releases/tag/v0.9.3)** — Released 2026-07-31 (PR #4993)

Key changes:
- **DeepSeek V4 Flash direct responses** and canonical tool catalog
- Rebranding: `codewhale` is now the public product name; legacy `deepseek-tui` npm package is deprecated with no further releases
- 72 single-concern commits assembled from clean isolated lanes, fast-forward only
- Candidate SHA: `80c66ddd735387669b846e0af15ad35765c1c3b6`

The legacy `deepseek` / `deepl` command paths from v0.8.x are being phased out.

## 3. Hot Issues

1. **[#4949 — Translation debate: "Constitution" as 宪法 vs. 协作准则](https://github.com/Hmbown/CodeWhale/issues/4949)** — Active community discussion (5 comments) on whether "Constitution" should be translated to the politically-sensitive 宪法 or the safer 协作准则 in Chinese docs. Author SparkofSpike (PR #4908) advocates for 宪法 to emphasize foundational authority, but concerns remain about political connotations. Highly relevant for the project's i18n direction.

2. **[#5007 — YouTuber uses Codex instead of CodeWhale as TUI for DeepSeek](https://github.com/Hmbown/CodeWhale/issues/5007)** — Community visibility concern: a popular YouTuber testing DeepSeek-v4-flash chose OpenAI's Codex over CodeWhale. The author notes CodeWhale is not the official TUI, but it highlights a marketing/adoption gap.

3. **[#5009 — SPAM: Ophthalmology billing](https://github.com/Hmbown/CodeWhale/issues/5009)** — Classic spam issue (medical billing services). Flagged as a reminder of the need for better spam filtering in the issue tracker.

4. **[#5003 — File edit tool fails on long Chinese-commented CRLF files](https://github.com/Hmbown/CodeWhale/issues/5003)** — Critical bug: `File` edit tool (`action=edit`/`patch`) repeatedly fails on ~700-line C files with Chinese comments and CRLF endings, causing **15+ failed attempts and 3 full `git checkout` rollbacks**. Model was forced to bypass the tool with an external Python script. High-impact reliability issue.

5. **[#5005 — Sandbox path whitelist for external build artifacts](https://github.com/Hmbown/CodeWhale/issues/5005)** — Xcode users can't access `~/Library/Developer/Xcode/DerivedData/` because the sandbox (`workspace-write` mode) restricts file access outside the workspace. Requests a configurable path allowlist.

6. **[#5000 — Interrupted assistant output should be a durable session item](https://github.com/Hmbown/CodeWhale/issues/5000)** — Engine design gap: when a turn is interrupted before `MessageComplete`, already-emitted text is lost from the authoritative session, breaking continuity for the next model turn.

7. **[#5002 — Tool not found: 'task' unavailable + Anthropic HTTP 400](https://github.com/Hmbown/CodeWhale/issues/5002)** — User-facing error: `Failed to locate tool: Tool 'task' is not available` alongside an Anthropic API error (HTTP 400). Suggests either a tool-resolution bug or an API-parameter mismatch.

8. **[#4999 — Benchmark/evaluation harness: deterministic, fail-closed, provenance-exact](https://github.com/Hmbown/CodeWhale/issues/4999)** — Maintainer-flagged reliability gap: the harness mixes ad hoc fixtures, unversioned trace formats, and incomplete lifecycle/cancellation handling, which undermines the trustworthiness of benchmark results as a product gate.

9. **[#4997 — GitHub Copilot as a named external ACP worker backend](https://github.com/Hmbown/CodeWhale/issues/4997)** — Proposal to consume Copilot's agent mode as a **named external ACP worker backend** (not a `ProviderKind`), with runtime-negotiated capabilities instead of hard-coded model rosters. Community appetite tracked in #2535.

10. **[#4382 — Remove unmaintained ttf-parser PDF dependency chain](https://github.com/Hmbown/CodeWhale/issues/4382)** — Cleanup request: v0.9.0 audit reports zero vulnerabilities, but `cargo audit` emits a maintenance warning for the `ttf-parser -> lopdf -> pdf-extract -> codewhale-tui` transitive path. Low urgency but good hygiene.

Also notable: **#5009** (spam above), **#4998** (headless OAuth with PKCE), **#4996** (protocol-neutral ACP client), **#4995** (semantic TUI graphics persistence), and **#4994** (explicit provider credential handoff).

## 4. Key PR Progress

1. **[#4993 — Release v0.9.3 (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/4993)** — The v0.9.3 integration and release train: 72 commits, DeepSeek V4 Flash responses, canonical tools. Merged.

2. **[#5008 — Actionable File edit diagnostics and stale-line-number tolerance (OPEN)](https://github.com/Hmbown/CodeWhale/pull/5008)** — Fixes #5003. Improves error messages when large replacements fail (100+ line patches, Chinese comments, CRLF endings) and adds tolerance for stale line numbers. Community-contributed by SparkofSpike.

3. **[#4977 — AltGr-typed "/" reaches composer instead of help (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/4977)** — Fixes #4723. On Windows ABNT2 layout, `AltGr+Q` (which produces `/`) was wrongly matched against the global `Ctrl-/` help chord, opening help every time the user typed a slash. Community-contributed by yyyCode.

4. **[#5001 — Measure circled digits and keycaps as 2 columns everywhere (OPEN)](https://github.com/Hmbown/CodeWhale/pull/5001)** — Fixes intermittent TUI rendering glitches (missing chars/phantom spaces) for Enclosed Alphanumerics (① ② Ⓐ), Dingbat circled digits (❶ ❷), and keycap sequences (1️⃣) on CJK terminals.

5. **[#5006 — Preserve long Windows user PATH during install (OPEN)](https://github.com/Hmbown/CodeWhale/pull/5006)** — NSIS `ReadRegStr` truncates long registry strings; installer replaced long PATH with only CodeWhale's bin directory. Community-contributed by XhesicaFrost.

6. **[#5004 — Restore the v0.9.3 rustdoc gate (CLOSED)](https://github.com/Hmbown/CodeWhale/pull/5004)** — Fixes a broken doc build by rendering the test-only synthetic-catalog helper as code instead of an intra-doc link; restores CI doc gate.

7. **[#5013 — Bump ratatui 0.30.0 → 0.30.2 (OPEN)](https://github.com/Hmbown/CodeWhale/pull/5013)** — Dependabot: TUI framework patch release. Ratatui is core to the TUI rendering, so this matters for stability.

8. **[#5010 — Bump actions/stale 10.4.0 → 11.0.0 (OPEN)](https://github.com/Hmbown/CodeWhale/pull/5010)** — Dependabot: major version jump for the stale-issue bot, likely with new behavior for auto-closing old issues — relevant given the high issue volume.

9. **[#5016 — Bump libc 0.2.186 → 0.2.189 (OPEN)](https://github.com/Hmbown/CodeWhale/pull/5016)** — Dependabot: routine dependency bump, but notable for Windows/Unix syscall surface stability.

10. **[#4910 — Docs: "Is Surf a Think? Why Make Mink?" (OPEN, Draft)](https://github.com/Hmbown/CodeWhale/pull/4910)** — A humorous/questioning draft PR asking about the deterministic verification surface. Author suggests it's "a question, not a contribution" — community-driven sanity check on testing practices.

## 5. Feature Request Trends

- **ACP (Agent Client Protocol) ecosystem uptake** — Three complementary asks: a protocol-neutral ACP client for external peers (#4996), GitHub Copilot as a named external ACP worker backend (#4997), and continued demand from #2535 (ACP+MCP). CodeWhale is clearly positioning as an ACP citizen, not just a DeepSeek TUI.

- **Headless & container-friendly auth** — #4998 (generic PKCE with manual redirect fallback) and #4994 (explicit credential handoff with pinned resolution) both address server/SSH/container environments where browser OAuth isn't possible.

- **Sandbox path configurability** — #5005 asks for a filesystem path whitelist/allowlist so the sandbox can access external build artifacts (e.g., Xcode DerivedData) without opening the entire filesystem.

- **Session durability and state persistence** — #5000 (durable interrupted output) and #4995 (semantic TUI graphics persistence) both push for first-class, restorable session state.

- **Deterministic verification surfaces** — #4999 (benchmark harness correctness) and the community "sanity check" PR #4910 both point to a desire for reproducible, fail-closed testing.

## 6. Developer Pain Points

1. **File-edit tool unreliability on large patches** — The #5003 report (15+ failed attempts, 3 git rollbacks, forced external Python workaround) is the most severe. The fix (#5008) is in review, but the pattern suggests the `File` tool needs more robust diff-application logic, especially for mixed-encoding (Chinese + CRLF) files.

2. **Windows-specific input and install issues** — Two active fixes target Windows: AltGr key collisions (#4977, now closed) and NSIS installer truncating long PATH values (#5006). Windows remains a second-class platform for terminal tools, but the community is actively patching.

3. **Unicode/CJK rendering glitches** — Circled digits and keycaps mis-measured as 1 column on CJK terminals (#5001) cause visible rendering artifacts. This is a recurring class of issues for multilingual TUI users.

4. **Missing external tooling access** — The sandbox blocks legitimate reads of build artifacts outside the workspace (#5005), forcing Xcode users to either disable the sandbox or write workarounds.

5. **Session continuity gaps** — Interrupted turns lose already-emitted text (#5000), making long-running conversations fragile. The engine lacks a first-class representation for partial output.

6. **Model capability/context constants scattered** — Issue #4599 and #4851 both flag that per-model facts are duplicated across crates, configs, and hardcoded literals, making maintenance error-prone.

---

*Digest compiled from github.com/Hmbown/CodeWhale data on 2026-08-01.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*