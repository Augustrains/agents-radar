# AI CLI Tools Community Digest 2026-06-23

> Generated: 2026-06-23 01:58 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report
**Date: 2026-06-23**

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem shows a bifurcated landscape: established players (Claude Code, GitHub Copilot CLI) focus on stability and incremental UX polish, while emerging tools (Kimi Code, Qwen Code, CodeWhale) invest heavily in provider extensibility and routing infrastructure. Platform-level convergence is visible across MCP protocol support, token-budget management, and provider flexibility — but each tool surfaces distinct approaches to subagent orchestration, session persistence, and configuration management. The most pressing shared challenge across all tools is **resource lifecycle management**: orphaned processes, memory leaks, and authentication state corruption appear ubiquitously, suggesting the industry is still converging on robust background-worker patterns.

## 2. Activity Comparison

| Tool | Issues Updated (24h) | PRs Updated (24h) | Release (24h) | Peak Community Concern |
|---|---|---|---|---|
| **Claude Code** | ~10 hot issues | 4 active | **v2.1.186** shipped | Copy/paste indentation (#18170, 265👍), iOS Remote Control crashes |
| **OpenAI Codex** | ~10 high-impact | 10 active | **3 pre-release Rust versions** | Rate-limit cost surge 10-20× (#28879, 239👍) |
| **Gemini CLI** | 50 issues received attention | 30 PRs updated | None | Subagent false success reports (#22323), agent hangs (#21409) |
| **GitHub Copilot CLI** | ~10 issues | 0 active | **v1.0.64-2, v1.0.64-3** | Auth loss on session resume (#3596, 11👍) |
| **Kimi Code** | 10 hot issues | 10 active | **v1.48.0** shipped | MCP config retention after deletion (#2457) |
| **OpenCode** | 10 hot issues | 10 active | None | Server memory leak 26.8 GiB (#33213) |
| **Pi** | 10 hot issues | 10 active | **v0.79.10** shipped | OpenAI Codex connection freezes (#4945, 30👍) |
| **Qwen Code** | 50+ issues | 50+ PRs | **2 builds failed** | Input validation gaps (11+ issues), release CI failures |
| **CodeWhale** | 10 hot issues | 10 active | **v0.8.64** | Provider routing complexity, Together route validation |

**Key Takeaways:**
- **Qwen Code** had the most raw activity (50+ issues and PRs), but much is "validation noise" — 20+ PRs from one contributor on integer boundaries, prompting maintainer countermeasures.
- **Gemini CLI** shows high maintenance velocity (30 PRs, 50 issues) despite no release — reflects deep architectural work.
- **Claude Code** and **OpenAI Codex** ship production releases but face acute community backlash on cost (Codex) and daily UX (Claude Code's copy/paste).

## 3. Shared Feature Directions

### Configuration & Settings
- **JSONC / comment support**: Claude Code (#17968, 87👍) — developers want inline documentation in settings.
- **Multi-format ignore files**: Qwen Code (#4653) — `.agentignore`, `.aiignore` alongside native format.
- **Machine-enforceable policies**: Claude Code (#70184) — enterprise/admin overrides for shared environments.

### MCP & Plugin Ecosystem
- **MCP client modernization**: OpenCode (#28567, 24👍) — catch up to MCP 2026 standard (streaming, notifications).
- **MCP server lifecycle management**: Kimi Code (#2457, #2469) — workspace-relative loading, purge mechanisms.
- **Plugin organization**: Copilot CLI (#1632, 20👍) — subfolder support for skills; CodeWhale — provider-scoped routing.

### Session & State Management
- **Ephemeral sessions**: OpenCode (#4489) — one-shot sessions for CI/CD; Pi (#5263) — in-session changes local only.
- **Cross-project session portability**: OpenCode (#31932), Codex (#15347) — sessions tied to projects, not movable.
- **Data loss after updates**: Claude Code (#12908 macOS, #53717 Windows) — sessions visible but content empty, no recovery.

### Observability & Cost Transparency
- **Usage/rate-limit visibility**: Codex (#28879) — unexpected 10-20× cost increase; Copilot (#3886) — restart consumes credits.
- **Completion notifications**: Codex (#3962, 177👍) — sound on finish; general async workflow demand.
- **Per-response timing**: Copilot (#3278) — elapsed time during generation.

### Reasoning Controls
- **Fine-grained thinking parameters**: Copilot (#3888) — independent control for Anthropic models; CodeWhale (#3222) — inline thinking rendering.
- **Reasoning effort strictness**: Kimi Code (#2465) — schema compliance for `reasoning_effort`.

### Token & Context Management
- **Token-budget compaction**: Codex (PRs #29521, #29520) — fresh context windows on compaction; Pi (#5291) — long-context stream management.
- **Context window metadata**: Codex (#29519) — persist context window IDs for observability.

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | CodeWhale |
|---|---|---|---|---|---|---|---|---|---|
| **Primary Strength** | Production stability, MCP auth | Token-budget optimization | Subagent orchestration | GitHub ecosystem integration | Provider API compliance | Plugin architecture | Local LLM flexibility | Chinese cloud ecosystem | Multi-provider routing |
| **Target User** | Professional developers | AI power users | Enterprise/GCP users | GitHub-centric teams | API-first developers | Advanced plugin devs | Open-source/local-first | Asian developer market | Cloud-agnostic power users |
| **Key Tech Approach** | Agent workflows, `/workflows` | Context compaction algorithms | A2A server protocol | Copilot agent mode | Jupyter/JSON integrity | Event-sourcing architecture | Extension/LSP-like | Qwen OAuth, custom providers | Provider-scoped routing (v0.8.65) |
| **Pain Point Emphasis** | Windows/iOS stability | Cost transparency | Subagent reliability | Auth state fragility | MCP config consistency | Memory leaks | Provider scalability | Input validation noise | Provider onboarding UX |
| **Release Cadence** | ~daily (minor patches) | ~weekly (alpha/beta) | Irregular (architectural) | ~weekly (stable) | ~biweekly | ~monthly | ~weekly | ~daily (nightly) | ~weekly (pre-release) |
| **Community Maturity** | Very high (265👍 top issue) | High (239👍 urgent) | Medium (8👍 top) | Medium (20👍 top) | Low (low engagement) | High (72👍 top issue) | Medium (36👍 top) | Medium (validation noise) | Low-medium (active contributors) |

**Notable Differentiators:**

- **Claude Code** has the most mature community (265👍 on its top issue) but also the longest-running unresolved pain point (#18170, copy/paste indentation, no fix in sight).
- **OpenAI Codex** is investing most heavily in token optimization (3 PRs on budget compaction) — unique focus on cost management.
- **Gemini CLI** has the deepest subagent reliability work (thought leakage fixes, false success detection) — unique agent-loop architecture.
- **CodeWhale** (formerly DeepSeek TUI) is the most ambitious on provider routing: explicit provider-scoped model picking, Chinese cloud vendor fixtures, Fleet worker execution — but still pre-1.0.
- **Qwen Code** shows signs of PR maintenance burden from automated/naive contributions — a growing problem for popular open-source repos.

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
- **Qwen Code**: 50+ issues and 50+ PRs in 24h, nightly builds, active maintainer response (PR #5723 adding batch-detection guards). Highest raw activity but noisy.
- **Gemini CLI**: 30 PRs and 50 issues touched without a release — deep architectural work on telemetry, settings merging, and MCP elicitation. Strong maintainer investment.
- **CodeWhale**: 10 PRs/day focused on architectural overhaul (v0.8.65 provider-scoped routing). Community contributing provider fixtures (Xiaomi, Alibaba, Baidu).

### Stable / Mature
- **Claude Code**: High-quality releases (v2.1.186 with MCP CLI auth), top-voted issue (#18170) at 265👍 reflects community size, not neglect. Windows/iOS issues suggest platform expansion strain.
- **OpenAI Codex**: Three pre-release Rust versions in 24h signals active development, but #28879 (rate-limit cost surge) is the most urgent community crisis across all tools — 239👍 in one day.
- **GitHub Copilot CLI**: Stable releases with incremental polish (HTTP proxy, inline images, OpenTelemetry). Low PR activity (0 in 24h) suggests mature codebase.

### Emerging / Building
- **Kimi Code**: Low community engagement (few 👍 on issues) but shipped meaningful fix (repeated-tool-call escalation, MCP auth). Still building user base.
- **Pi**: Active provider expansion (Merge Gateway, Anthropic Vertex, auto-routing) with 36👍 top issue. Production-quality but small community.
- **OpenCode**: High community maturity (72👍 on memory megathread) but critical infrastructure issues (26.8 GiB memory leak) undermine confidence.

## 6. Trend Signals

### Industry Trends from Community Feedback

1. **Cost management is the #1 emerging tension.** OpenAI Codex's 10-20× cost surge (#28879) without announcement has damaged trust in flat-rate pricing. Communities across tools are demanding usage transparency, credit accounting, and budget controls. Token-budget compaction (Codex PRs) and session-level thinking controls (Copilot #3888) are direct responses.

2. **MCP is becoming universal infrastructure, but implementation quality varies wildly.** Every tool supports MCP, but regressions (Kimi Code config retention, OpenCode image attachment loss, Copilot variable interpolation) show protocol adoption is outpacing testing. The community is demanding lifecycle management, workspace-relative loading, and standard compliance.

3. **Windows remains a second-class citizen.** Claude Code (blank screen, orphaned processes, data loss), Codex (GPU/CPU idle load), and Copilot (platform-specific bugs) all have Windows-specific pain points. Developers on Windows are experiencing a "care of issues" across the board.

4. **Subagent reliability is the next frontier.** Gemini CLI (#22323 false success, #21409 indefinite hangs) and Copilot's agent mode highlight that autonomous subagent execution is the most fragile part of the stack. The industry hasn't converged on failure detection, recovery, or observability patterns.

5. **Local/first-party model integration is still underserved.** Pi's #3357 (local LLM provider, 36👍) and CodeWhale's provider fixture contributions show strong demand for running open-source models. The provider abstraction layer is still too complex for average users.

6. **Chinese cloud ecosystem is a growing but fragmented market.** Qwen Code and CodeWhale are actively building for Alibaba, Baidu, Xiaomi, and SiliconFlow integrations. Western tools (Claude Code, Codex, Copilot) have no equivalent support.

7. **Session persistence fragility is universal.** Data loss after updates (Claude Code macOS #12908, Windows #53717), thread disappearance (Codex #15406), and authentication state corruption (Copilot #3596) — the "session" abstraction is not yet robust across restarts, updates, or service incidents.

### Reference Value for Developers

- **If cost sensitivity is critical**: Watch OpenAI Codex's token-budget compaction work (PRs #29521, #29520) — the leading implementation of fine-grained budget accounting.
- **If multi-provider flexibility matters**: CodeWhale's v0.8.65 provider-scoped routing architecture is the most ambitious, though still pre-1.0.
- **If enterprise compliance is non-negotiable**: Claude Code's policy layer request (#70184) and Gemini CLI's telemetry fixes (PR #28093) represent the most mature thinking on admin controls.
- **If you use Windows**: Be prepared for ongoing issues across all tools. Claude Code has the most complete issue list but no fixes in sight.
- **If you build MCP tools**: Expect integration brittleness. Test across Claude Code, Codex, and OpenCode — the three most MCP-intensive platforms.
- **If you need CICD integration**: OpenCode's ephemeral session request (#4489) and Pi's RPC exposure (#5810) are the clearest feature signals for programmatic tooling.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot:** github.com/anthropics/skills | 2026-06-23

---

## 1. Top Skills Ranking

**1. skill-creator fix: run_eval.py 0% recall bug** (PR #1298) — **Open**
- **Functionality:** Fixes the skill-creator's evaluation pipeline where `run_eval.py` always reports 0% recall due to improper artifact installation, Windows stream reading issues, trigger detection failures, and parallel worker logic.
- **Discussion:** Links to Issue #556 (12 comments) as the canonical bug report. Multiple independent reproductions confirm the optimizer is "optimizing against noise." The PR is the direct fix for the most critical bug in the skill ecosystem toolchain.
- **Status:** Open, updated June 22.
- **GitHub:** [PR #1298](https://github.com/anthropics/skills/pull/1298)

**2. document-typography skill** (PR #514) — **Open**
- **Functionality:** Typographic quality control preventing orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — issues that "affect every document Claude generates."
- **Discussion:** Positions itself as a universal document quality layer. No opposition; the value proposition is self-evident.
- **Status:** Open since March 4.
- **GitHub:** [PR #514](https://github.com/anthropics/skills/pull/514)

**3. ODT skill — OpenDocument text creation** (PR #486) — **Open**
- **Functionality:** Full ODF lifecycle support: create, fill, read, and convert .odt/.ods files. Triggers on "ODT", "ODS", "LibreOffice", or any open-source document request.
- **Discussion:** Addresses a clear interoperability gap — no native ODF support existed. No controversy noted.
- **Status:** Open since March 1, updated April 14.
- **GitHub:** [PR #486](https://github.com/anthropics/skills/pull/486)

**4. ServiceNow platform skill** (PR #568) — **Open**
- **Functionality:** Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD, CSM, SPM/PPM, Vulnerability Response, Security Incident Response, and IntegrationHub.
- **Discussion:** By far the most ambitious enterprise platform skill. No merged enterprise integration skills of this scale exist yet.
- **Status:** Open since March 8, updated April 23.
- **GitHub:** [PR #568](https://github.com/anthropics/skills/pull/568)

**5. AURELION skill suite** (PR #444) — **Open**
- **Functionality:** Four skills — aurelion-kernel (structured cognitive framework), aurelion-advisor, aurelion-agent, aurelion-memory — forming a professional knowledge management and AI collaboration system.
- **Discussion:** The most complex multi-skill proposal. Introduces a proprietary cognitive architecture; community may evaluate whether the framework is too opinionated.
- **Status:** Open since February 21, updated May 6.
- **GitHub:** [PR #444](https://github.com/anthropics/skills/pull/444)

**6. testing-patterns skill** (PR #723) — **Open**
- **Functionality:** Coverage of the full testing stack — testing philosophy (Testing Trophy model), unit testing (AAA pattern), React component testing, and coverage guidance.
- **Discussion:** Addresses a core developer need. No standard testing skill currently exists in the collection.
- **Status:** Open since March 22, updated April 21.
- **GitHub:** [PR #723](https://github.com/anthropics/skills/pull/723)

**7. skill-quality-analyzer & skill-security-analyzer** (PR #83) — **Open**
- **Functionality:** Meta-skills for evaluating other skills across five quality dimensions (20% structure, examples, resources) and security vulnerability analysis.
- **Discussion:** The longest-running open skill proposal (since November 2025). May be blocked by pending skill-creator tooling improvements.
- **Status:** Open, updated January 7.
- **GitHub:** [PR #83](https://github.com/anthropics/skills/pull/83)

---

## 2. Community Demand Trends

From top Issues (sorted by comments), the community's most anticipated directions are:

| Demand Area | Key Issue | Discussion Heat |
|---|---|---|
| **Org-wide skill sharing** | #228 — enable org sharing without manual .skill file transfers | 14 comments, 7 👍 |
| **Skill-creator bug fixes** | #556 — 0% trigger rate prevents all skill optimization | 12 comments, 7 👍 |
| **Trust & security** | #492 — namespace impersonation and trust boundary abuse | 9 comments |
| **Agent governance** | #412 — safety patterns for AI agent systems | 6 comments |
| **Duplicate management** | #189 — document-skills and example-skills install identical content | 6 comments, 9 👍 |
| **Windows compatibility** | #1061 — skill-creator scripts fail on Windows | 3 comments |
| **MCP exposure** | #16 — expose Skills as MCP protocols | 4 comments |

**Key themes:**
1. **Tooling reliability** dominates — the skill-creator evaluation loop is fundamentally broken on both macOS (0% recall) and Windows (pipe/encoding errors).
2. **Enterprise governance** is rising sharply — security, namespace trust, agent safety, and org sharing are becoming critical concerns.
3. **Platform interoperability** — connecting Skills to MCP, AWS Bedrock, and SharePoint is emerging as a long-term need.

---

## 3. High-Potential Pending Skills

These open PRs have active discussion and are likely to land soon:

1. **document-typography** (PR #514) — Lightweight, universal value; no blockers. **Likely merge target.**
2. **ODT skill** (PR #486) — Fills a clear format gap. Awaiting review.
3. **testing-patterns** (PR #723) — High developer value; no architectural controversy.
4. **skill-creator Windows fixes** (PR #1050, PR #1099) — Lower priority due to ongoing parallel PRs.
5. **CONTRIBUTING.md** (PR #509) — Direct community health fix; addresses Issue #452. **Should merge quickly.**

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill evaluation toolchain — the skill-creator's 0% recall bug (PR #1298, Issue #556) is the single largest blocker preventing the ecosystem from scaling, as no skill description can be optimized until the optimizer itself works correctly.**

---

# Claude Code Community Digest — 2026-06-23

## Today's Highlights

Claude Code **v2.1.186** shipped with two notable quality-of-life improvements: CLI-based MCP authentication for SSH workflows and status filtering in the agent workflows view. On the bug front, a critical cluster of **iOS Remote Control crashes** (Issues #70108, #70165, #70182, #70164) has erupted from the latest app update, while the long-running top-voted issue on copy/paste indentation (#18170, 265 👍) continues to frustrate users.

---

## Releases

- [**v2.1.186**](https://github.com/anthropics/claude-code/releases/tag/v2.1.186)
  - **`claude mcp login <name>` / `claude mcp logout <name>`** — authenticate MCP servers from the CLI without opening the interactive `/mcp` menu. Supports `--no-browser` stdin redirect for completing auth over SSH.
  - Press **`f`** in the `/workflows` agent to filter by status.

---

## Hot Issues (Top 10 by Community Impact)

1. **[#18170 — Copy/paste from terminal includes unwanted indentation and trailing spaces](https://github.com/anthropics/claude-code/issues/18170)**  
   *265 👍, 124 comments* — The longest-running open issue. Pasting code from Claude Code output strips formatting? Nope — it *adds* leading tabs and trailing spaces. A daily pain point for anyone using the terminal, and the community is vocal. No fix in sight.

2. **[#60226 — Claude states its own analysis is unfounded, then completes it anyway](https://github.com/anthropics/claude-code/issues/60226)**  
   *45 comments* — A fascinating agent-level bug: Claude self-identifies logical gaps in its reasoning, documents them, then proceeds to output the analysis as if the gaps don't exist. Distinct from the "act-first" bias reported elsewhere; hits at core reasoning vs. output-gating issues.

3. **[#17968 — Support JSONC format for settings files (settings.jsonc)](https://github.com/anthropics/claude-code/issues/17968)**  
   *87 👍* — JSON doesn't support comments. Developers want `settings.jsonc` to document configuration decisions inline. A straightforward, high-signal request that keeps gaining traction.

4. **[#12908 — Conversation History disappeared after update](https://github.com/anthropics/claude-code/issues/12908)**  
   *18 👍, 14 comments* — macOS users losing all session history after auto-updates. Persistence fragility remains a recurring theme.

5. **[#53717 — Windows: all message content missing after auto-update](https://github.com/anthropics/claude-code/issues/53717)**  
   *Windows data-loss counterpart to #12908* — Sessions appear in the sidebar but message content is gone; JSONL files are empty. Affected users have no recovery path.

6. **[#51143 — Claude Desktop persistent blank/white screen on Windows](https://github.com/anthropics/claude-code/issues/51143)**  
   *15 comments* — Cowork unusable; multiple reinstalls no help. Desktop app stability on Windows continues to generate heat.

7. **[#68394 — Windows: agent session processes + MCP fleets not reaped on session end](https://github.com/anthropics/claude-code/issues/68394)**  
   *3 comments (but high severity)* — Each session on Windows leaves orphaned `claude.exe` processes and MCP server fleets. They accumulate across launches until the user manually kills them. Resource leak, not just a cosmetic issue.

8. **[#69592 — "You've hit your session limit" resets earlier than expected](https://github.com/anthropics/claude-code/issues/69592)**  
   Users hitting 5-hour limits suspiciously early. References a public social post from @ClaudeDevs, suggesting a known server-side issue that may affect rate-limit accounting.

9. **[#70108 / #70165 / #70182 / #70164 — iOS app crashes on Remote Control sessions](https://github.com/anthropics/claude-code/issues/70108)**  
   *Cluster of 4 related iOS regression bugs* — The 1.260618.0 iOS update introduced hard crashes when opening Remote Control sessions, tapping "New Code Session," or linking from the Code tab. One report mentions a Swift KeyPath metadata stack overflow. Affects Cowork users heavily.

10. **[#67021 — Bundled ugrep OOMs the host on certain regex patterns](https://github.com/anthropics/claude-code/issues/67021)**  
    *1 comment, but impactful* — `ugrep` with two bounded `{0,N}` intervals blows up DFA construction to multiple GB of RAM. If Claude Code auto-generates such a pattern, it can take down the entire host.

---

## Key PR Progress

1. **[#70173 — Fix `/clean_gone` detection of `[gone]` branches](https://github.com/anthropics/claude-code/pull/70173)**  
   Root cause: `git branch -v` only shows one line per branch and may not include remote tracking info. The fix switches to `git branch -vv` to reliably see `[gone]`. Currently `/clean_gone` never actually deletes anything — this is a straight bugfix.

2. **[#63686 — Bump stale/autoclose timeouts from 14 to 90 days](https://github.com/anthropics/claude-code/pull/63686)**  
   A process change: currently issues go stale after 14 days of inactivity and auto-close soon after. The community (and this PR) argue that's far too aggressive for a developer tool where issues need time to gather repros and discussion. 90 days would give more breathing room.

3. **[#70074 — Fix stale marketplace name in plugin-dev README](https://github.com/anthropics/claude-code/pull/70074)**  
   The plugin marketplace was renamed from `claude-code-marketplace` to `claude-code-plugins`, but the README still references the old name. Simple docs fix, but important for plugin developers onboarding today.

4. **[#70066 — Update plugin-dev README install instructions](https://github.com/anthropics/claude-code/pull/70066)**  
   Companion to #70074: updates install examples to use the official marketplace name and switches `cc --plugin-dir` to `claude --plugin-dir`. Clarifies contribution flow.

---

## Feature Request Trends

1. **JSONC / Comment support in settings** — `settings.jsonc` (#17968, 87 👍) has become a clear community consensus. Developers want inline documentation for their Claude Code configuration without resorting to `_comment` hacks.

2. **Machine-level enforceable policies** — #70184 requests a facility-admin policy layer that overrides user settings, specifically for HPC / shared infrastructure environments. Enterprise and academic users need this for compliance.

3. **Edit amendment before write** — #70188 proposes a `$EDITOR` hook: when Claude proposes a file edit that's 90% correct, users want to tweak it in their editor rather than reject and re-prompt. A workflow efficiency ask.

4. **Configurable git polling interval** — #70186 requests a `gitPollingIntervalMs` setting (default 0 to disable). Multiple concurrent sessions in the same repo cause `.git/index.lock` contention from ~20-second polling.

5. **Feature parity with Ultracode** — #70190 is vague but indicates a general desire to match the capabilities of the closed-source Ultracode fork.

---

## Developer Pain Points

- **Windows stability is the #1 reliability concern**: blank screens (#51143), data loss on update (#53717), orphaned processes (#68394), cross-device rename errors (#66159), persistent "update available" notification (#63238). Windows users are experiencing a care of issues.

- **iOS app is currently broken for Remote Control**: four separate crash reports (multiple submission but also multiple different triggers: tapping a session, creating a new session, linking from Code tab). Cowork / mobile pairing users are blocked.

- **Data loss after updates keeps recurring**: both macOS (#12908) and Windows (#53717) users report sessions that appear in the sidebar with empty message histories. No recovery path mentioned in any resolution.

- **Copy/paste degrades daily terminal use**: #18170 (265 👍) is the most-upvoted open issue. Terminal output includes unwanted formatting artifacts when copied — this touches every single user, every single day.

- **Rate-limit and session-limit confusion**: #69592 and #70183 both report hitting limits that don't align with documented policies. Until Anthropic clarifies server-side rate accounting, users are left guessing whether it's a bug or a policy change.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-23

## Today's Highlights

Rate-limit cost surges dominate community concern this week, with Issue #28879 reporting a 10–20× per-token cost increase on GPT-5.5 draining Plus budgets in 2-3 prompts. On the development front, significant work continues on token-budget compaction (PRs #29521, #29520), MCP infrastructure improvements, and the code mode host handshake protocol (PR #29515). The team shipped three pre-release Rust versions while the community flagged persistent Crashpad dump accumulation and idle GPU/CPU usage on Windows.

## Releases

- **rust-v0.142.0**: `/usage` now shows and redeems earned usage-limit reset credits with confirmation, retry, and refreshed availability states (#28154, #28793). `/plugins` organizes remote plugins into OpenAI Curated, Workspace, and Shared with me sections.
- **rust-v0.143.0-alpha.1 / alpha.2**: Pre-release milestones.
- **rust-v0.142.0-alpha.11 / alpha.12**: Pre-release milestones.

## Hot Issues

1. **[#28879] Rate-limit cost per token jumped ~10-20x since June 16**  
   https://github.com/openai/codex/issues/28879  
   The most urgent issue this week (117 comments, 239👍). Plus plan users report GPT-5.5 budgets draining in 2-3 prompts instead of 20+. Session logs confirm limit-% consumed per token increased 10-20× with no configuration change. Community growing increasingly vocal about cost transparency.

2. **[#3962] Play sound when Codex finishes a prompt**  
   https://github.com/openai/codex/issues/3962  
   Long-standing enhancement request (52 comments, 177👍). Users want an optional audible completion signal when running background tasks. High demand from developers who switch contexts during long prompts.

3. **[#25921] Crashpad pending dumps grow without limit: +5GB/day**  
   https://github.com/openai/codex/issues/25921  
   Codex Desktop continuously generates `.dmp` and `_sidecar.json` files under `Crashpad/pending`. One user reported 54,504 files consuming 4.9GB in a single day. Serious storage and performance concern for macOS users.

4. **[#15347] Support moving/remapping workspace folder without losing threads**  
   https://github.com/openai/codex/issues/15347  
   When a workspace is moved to a new folder, importing it doesn't carry over existing threads. Affects developers reorganizing projects. 15 comments, ongoing discussion.

5. **[#17066] Marketplace local plugin path "./" cannot reference repository root**  
   https://github.com/openai/codex/issues/17066  
   `resolve_plugin_source_path()` rejects any local path resolving to the marketplace root directory, making it impossible to register a plugin at root level. Closed with fix merged.

6. **[#28504] Pro account missing Codex reset bank and invite/referral entitlement**  
   https://github.com/openai/codex/issues/28504  
   Pro ($200/month) users report missing reset bank and referral credits. Affects Windows users specifically. 6 comments, 6👍.

7. **[#21167] Desktop reconnect loop on new/restarted conversations**  
   https://github.com/openai/codex/issues/21167  
   Reproducible reconnect loops when starting new or resuming old conversations. Not caused by VPN or cache. 4 comments, affecting multiple users.

8. **[#29281] Windows 11: sustained fan noise and GPU/CPU activity while idle**  
   https://github.com/openai/codex/issues/29281  
   After recent update (26.616.4196.0), Codex causes continuous high resource usage even when idle. Affects thermal and battery performance. Published yesterday, already 3 comments and 2👍.

9. **[#14396] "failed to resume task" on all sessions after service incident**  
   https://github.com/openai/codex/issues/14396  
   Enterprise and Pro users experiencing persistent "failed to resume task" errors on macOS after a service incident. 2 comments, 7👍. Indicates lingering server-side state issues.

10. **[#15406] Threads randomly disappear from history**  
    https://github.com/openai/codex/issues/15406  
    Threads vanish from history without explicit deletion. Suspected sync/cache issue. 2 comments, 10👍. Closed but underlying concern remains.

## Key PR Progress

1. **[#29521] core: reset context for token budget compaction**  
   https://github.com/openai/codex/pull/29521  
   When token-budget is enabled, compaction now starts a fresh context window (like `new_context`) instead of carrying history forward. Critical for keeping token usage within budget.

2. **[#29520] Scope token-budget accounting to body-after-prefix window**  
   https://github.com/openai/codex/pull/29520  
   Ensures `BodyAfterPrefix` correctly charges the configured body budget against growth after the carried harness prefix, while respecting the full model context window as safety cap.

3. **[#29519] Persist initial context window metadata**  
   https://github.com/openai/codex/pull/29519  
   Makes context-window IDs visible to rollout JSONL consumers by persisting initial window identity in session files, not just after compaction.

4. **[#29515] define code mode host handshake protocol**  
   https://github.com/openai/codex/pull/29515  
   Adds validated protocol-version, capability, and session identifier types with explicit `ClientToHost`/`HostToClient` envelopes for connection negotiation. Foundation for structured code mode.

5. **[#29493] mcp: accept foreign absolute cwd for remote stdio**  
   https://github.com/openai/codex/pull/29493  
   Fixes cross-platform MCP server startup where Windows absolute paths (e.g., `C:\Users\...`) were rejected by POSIX orchestrators. Built on #29501.

6. **[#27466] Trace exec-server JSON-RPC requests**  
   https://github.com/openai/codex/pull/27466  
   Propagates W3C trace context across JSON-RPC boundaries, enabling correlation of client and server work for diagnosing latency and failures across local/remote transports.

7. **[#28598] right-size Rust test targets**  
   https://github.com/openai/codex/pull/28598  
   Bazel timeout warnings obscure test failures; this PR defaults Rust tests to `small` with per-target size overrides. Improves CI signal clarity.

8. **[#29514] skip initial rollout budget prefill**  
   https://github.com/openai/codex/pull/29514  
   Prevents charging the initial prompt prefill against the rollout budget for each thread, only charging sampled output on the first response. Optimizes budget consumption.

9. **[#28271] Flatten MCP namespace tools for unsupported providers**  
   https://github.com/openai/codex/pull/28271  
   Fixes #26234 — some Responses API providers don't understand Codex's `type: "namespace"` tool wrapper. This adds a provider capability to flatten namespaced MCP tools.

10. **[#26705] TUI Plugin Sharing 5 - polish remote plugin catalog rows**  
    https://github.com/openai/codex/pull/26705  
    Final PR in the plugin sharing stack. Admin-disabled plugins read as blocked/view-only, admin-installed plugins sort correctly. Polish for the remote plugin catalog UX.

## Feature Request Trends

- **Completion notifications**: Issue #3962 (sound on finish) and #17716 (desktop notifications for approval requests) reflect strong demand for non-blocking async workflows.
- **Workspace portability**: Moving/remapping workspace folders without losing thread history (#15347) appears alongside session resumption bugs (#14396, #21167), indicating fragility in session persistence.
- **Plugin ecosystem improvements**: Better local plugin path handling (#17066), plugin catalog UI polish (PR #26705), and cross-platform MCP support (PR #29493) show the team investing in extensibility.
- **Usage transparency**: Growing demand for clear cost/usage visibility, driven by rate-limit changes (#28879) and entitlement issues (#28504).

## Developer Pain Points

1. **Rate-limit unpredictability**: The 10-20× cost increase (#28879) is the standout complaint — no configuration change, no announcement, just sudden depletion. Undermines trust in flat-rate pricing.
2. **Resource leaks**: Crashpad dump accumulation (+5GB/day, #25921) and idle GPU/CPU load on Windows (#29281) indicate poor resource lifecycle management, especially problematic for laptop users.
3. **Session fragility**: Threads disappearing (#15406), reconnect loops (#21167), resume failures (#14396) — session state management across app restarts and service incidents remains unreliable.
4. **Cross-platform inconsistencies**: Windows users face unique issues: splash screen hangs (#29386), network path normalization (#13846), browser plugin registration (#25353), and approval prompts despite full access (#29043).
5. **Context window confusion**: Frequent auto-compaction (#14447) followed by nearly full context windows frustrates users who expect compaction to free space. PRs #29521 and #29520 directly address this.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-23

## Today's Highlights

No new releases landed in the last 24 hours, but the project saw significant maintenance activity with 30 PRs updated and 50 issues receiving attention. Key themes include **subagent reliability** (false success reports, hangs, tool selection), **memory system bugs** (indefinite retries, silent patch corruption), and a batch of critical **telemetry and startup ordering fixes** landing in the core.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

### 1. Subagent recovery after MAX_TURNS reported as success
**#22323** — `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit the turn limit and performed zero analysis. This masks real failures from users. Community gave 2 👍.  
🔗 [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. Generalist agent hangs forever
**#21409** — The CLI hangs indefinitely when deferring to the generalist agent for simple tasks like folder creation. User reports waiting up to an hour. Workaround: instruct the model not to use subagents. Highest community engagement with 8 👍.  
🔗 [Issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. Shell command execution stuck on "Waiting input"
**#25166** — After executing trivial commands that cannot prompt for input, the CLI shows `Waiting input` indefinitely. 3 👍 suggest this is a common frustration for daily use.  
🔗 [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 4. Browser subagent fails on Wayland
**#21983** — The browser agent crashes on Wayland display servers, a blocker for Linux users outside X11 environments.  
🔗 [Issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 5. Model doesn't use skills and sub-agents autonomously
**#21968** — Custom skills (e.g., `gradle`, `git`) and sub-agents are ignored by the model unless explicitly instructed. The model fails to recognize when a skill's description matches the task.  
🔗 [Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 6. Auto Memory retries low-signal sessions indefinitely
**#26522** — Sessions that the extraction agent deems low-signal remain unprocessed forever, causing endless re-scans of the same transcripts. Memory system quality issue flagged by SandyTao520.  
🔗 [Issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 7. Deterministic redaction and Auto Memory logging needed
**#26525** — Secrets are redacted *after* content is already in model context. Also, existing skill transcripts may be logged. Security concern for enterprise users.  
🔗 [Issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)

### 8. 400 error with >128 tools
**#24246** — CLI returns a 400 error when more than 128 tools are available. No smart tool filtering exists.  
🔗 [Issue #24246](https://github.com/google-gemini/gemini-cli/issues/24246)

### 9. Model creates temporary scripts in random locations
**#23571** — When restricted from shell execution, the model scatters edit scripts across directories, making workspace cleanup painful.  
🔗 [Issue #23571](https://github.com/google-gemini/gemini-cli/issues/23571)

### 10. AST-aware file reads and search exploration
**#22745** — Epic tracking whether AST-aware tools can reduce token waste, improve method-boundary reading, and enable smarter codebase navigation. 1 👍 from the community.  
🔗 [Issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)

---

## Key PR Progress

### 1. Drop late tool calls after SIGINT cancellation
**#28096** — Prevents tool-call chunks from executing *after* the user cancels with Ctrl+C. Closes a race condition where side effects leaked post-cancellation.  
🔗 [PR #28096](https://github.com/google-gemini/gemini-cli/pull/28096)

### 2. Fix Jupyter Notebook and JSON corruption in write_file
**#28000** — `write_file` was silently corrupting `.ipynb` and `.json` files, causing environments like Colab to revert to checkpoints. Closed and merged.  
🔗 [PR #28000](https://github.com/google-gemini/gemini-cli/pull/28000)

### 3. Defensive path resolution for `@`-prefixed file references
**#28053** — Fixes "File not found" when the model uses `@policies/new-policies.txt` syntax. Large PR (size/xl), still open.  
🔗 [PR #28053](https://github.com/google-gemini/gemini-cli/pull/28053)

### 4. Strip thoughts from scrubbed history turns
**#27971** — Resolves "thought leakage" where internal model monologues leak into plain-text history, causing infinite loops. This is a deep agent-quality fix.  
🔗 [PR #27971](https://github.com/google-gemini/gemini-cli/pull/27971)

### 5. Deep-merge user and workspace settings for A2A server
**#28094** — Shallow spread was dropping nested settings (`tools`, `telemetry`, etc.). Now correctly merges nested objects.  
🔗 [PR #28094](https://github.com/google-gemini/gemini-cli/pull/28094)

### 6. Buffer chat compression telemetry until SDK init
**#28093** — Telemetry was being emitted before the OpenTelemetry SDK finished initialization, causing lost data. Critical for enterprise deployments.  
🔗 [PR #28093](https://github.com/google-gemini/gemini-cli/pull/28093)

### 7. Trust dialog discloses wrong hook shape
**#27915** — The workspace-trust dialog displayed the *inverse* of the hooks that would actually run. A security fix — the UI could show no commands while executing arbitrary shell.  
🔗 [PR #27915](https://github.com/google-gemini/gemini-cli/pull/27915)

### 8. Fix empty parts arrays misclassified as function calls
**#28068** — `isFunctionCall()` and `isFunctionResponse()` returned `true` for messages with empty `parts` arrays due to `[].every()` returning `true` in JavaScript.  
🔗 [PR #28068](https://github.com/google-gemini/gemini-cli/pull/28068)

### 9. Implement MCP elicitation (form + url) capability
**#28089** — Implements the latest MCP spec for form-based and URL-based user interaction elicitation in the core MCP client.  
🔗 [PR #28089](https://github.com/google-gemini/gemini-cli/pull/28089)

### 10. GCP project ID validation fix in memory
**#27916** — Prevents auto-memory from storing GCP display names/aliases instead of project IDs, which caused 403 and CONSUMER_INVALID errors.  
🔗 [PR #27916](https://github.com/google-gemini/gemini-cli/pull/27916)

---

## Feature Request Trends

- **Agent self-awareness** — Multiple requests (#21432, #21409) for the model to understand its own capabilities, flags, hotkeys, and tool boundaries.
- **Subagent observability** — Users want subagent trajectories visible via `/chat share` and included in `/bug` reports (#22598, #21763).
- **AST-aware code navigation** — Exploration of tilth/glyph for smarter file reads and method-boundary resolution (#22745, #22746).
- **Memory system transparency** — Need for quarantining invalid patches, surfacing extraction failures, and preventing indefinite retries (#26523, #26522).
- **Deterministic secret redaction** — Moving redaction to before content reaches model context (#26525).

---

## Developer Pain Points

1. **Subagent reliability is the #1 frustration** — False success reports (#22323), indefinite hangs (#21409), unauthorized activation after update (#22093), and failure to use custom skills (#21968) dominate the issue tracker.
2. **Shell execution brittleness** — Commands hanging on "Waiting input" after completion (#25166), stuck interactive prompts (#22465), and scattered temp scripts (#23571) disrupt daily workflows.
3. **Configuration and tool management** — Symlinks not recognized as agents (#20079), settings.json overrides ignored by browser agent (#22267), and 400 errors with >128 tools (#24246).
4. **Terminal and UI regressions** — Corruption after exiting external editors (#24935), flicker on resize (#21924), and incorrect `\n` escape behavior (#22466).
5. **Memory system opacity** — Low-signal sessions retried forever (#26522), invalid patches silently skipped (#26523), and secrets exposed before redaction (#26525).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date: 2026-06-23**

## Today's Highlights

Two minor patch releases (v1.0.64-2 and v1.0.64-3) shipped today, adding HTTP(S) proxy settings, inline image rendering, and conversation scrollbar controls. A fresh triage issue (#3888) asks for independent control over extended thinking for Anthropic models, signaling growing demand for fine-grained reasoning controls. Meanwhile, the ongoing authentication bug (#3596) upon session resume continues to attract community attention with 11 upvotes.

## Releases

Two new versions were published in the last 24 hours:

**v1.0.64-3** — [Release Link](https://github.com/github/copilot-cli/releases/tag/v1.0.64-3)
- **Added:** HTTP(S) proxy now configurable via user setting
- **Fixed:** Resume sessions by name even when the name contains spaces
- **Fixed:** Hidden unsupported slash commands in remote-hosted sessions

**v1.0.64-2** — [Release Link](https://github.com/github/copilot-cli/releases/tag/v1.0.64-2)
- **Added:** Setting to hide the conversation scrollbar
- **Added:** Inline image rendering directly in the CLI
- **Added:** Argument-hint frontmatter support for skills
- **Added:** OpenTelemetry improvements — chat spans after successful compaction now carry `gen_ai.conversation.compacted=true` and emit summary as `CompactionPart`

## Hot Issues

1. **#3596** — [OPEN] **Error loading model list: Not authenticated when resuming sessions**  
   *Area: authentication, sessions, models*  
   Users report that resuming a specific session breaks the `/model` command with authentication errors, while fresh sessions work fine. High community engagement with 11 👍.  
   [Issue Link](https://github.com/github/copilot-cli/issues/3596)

2. **#1632** — [OPEN] **Support subfolders for skills**  
   *Area: plugins*  
   The most upvoted open issue (20 👍) asks for hierarchical organization of skills. Users with 10+ custom skills find flat folder structures unmanageable.  
   [Issue Link](https://github.com/github/copilot-cli/issues/1632)

3. **#3888** — [OPEN] **Expose extended thinking independent of reasoning effort**  
   *Area: triage*  
   Fresh request (filed today) asking for separate controls for Anthropic models' thinking parameter vs. reasoning effort. Currently, CLI only exposes effort.  
   [Issue Link](https://github.com/github/copilot-cli/issues/3888)

4. **#3162** — [CLOSED] **Registry-listed MCP servers falsely reported as blocked by policy**  
   *Area: mcp*  
   Fixed in a prior release, but this bug caused confusion for users relying on custom MCP servers from the registry. 7 comments and 1 👍.  
   [Issue Link](https://github.com/github/copilot-cli/issues/3162)

5. **#3278** — [OPEN] **Display per-response elapsed time during and after generation**  
   *Area: terminal-rendering*  
   Users want visible timing for long-running operations, especially in autopilot mode where agents may work autonomously for minutes.  
   [Issue Link](https://github.com/github/copilot-cli/issues/3278)

6. **#3887** — [OPEN] **`/mcp` install from registry doesn't interpolate `packageArguments` variables**  
   *Area: triage*  
   Raw variable placeholders (e.g., `{ado_org}`) get written literally into config files instead of being resolved, breaking MCP server installations.  
   [Issue Link](https://github.com/github/copilot-cli/issues/3887)

7. **#3886** — [OPEN] **Restarting copilot consumes AI credits**  
   *Area: sessions, models*  
   `/restart` and `/resume` commands appear to consume ~174 AI credits consistently, which users consider wasteful since the session isn't performing new work.  
   [Issue Link](https://github.com/github/copilot-cli/issues/3886)

8. **#2399** — [OPEN] **Use sparse checkout for plugin installs**  
   *Area: plugins, installation*  
   Suggests using `git sparse-checkout` instead of full clones for plugin installation to avoid downloading tests, CI configs, and other non-essential files.  
   [Issue Link](https://github.com/github/copilot-cli/issues/2399)

9. **#1579** — [OPEN] **Copilot CLI ignores MCP server "instructions" returned during initialization**  
   *Area: configuration, mcp*  
   MCP servers can return initialization instructions per protocol spec, but the CLI discards them, potentially degrading LLM performance. 3 👍.  
   [Issue Link](https://github.com/github/copilot-cli/issues/1579)

10. **#3883** — [OPEN] **i18n support for top 10 most-spoken languages**  
    *Area: theming-accessibility*  
    Community requests localization for UI text (menus, prompts, errors, help). Currently all English-only.  
    [Issue Link](https://github.com/github/copilot-cli/issues/3883)

## Key PR Progress

No pull requests were updated in the last 24 hours. The project appears to be in a maintenance/stable phase with no active PR activity to report.

## Feature Request Trends

The most-requested feature directions across all open issues this week are:

1. **Timing & observability** — Multiple requests (#3278, #3111, #3055) ask for elapsed-time indicators during agent thinking, shell commands, and response generation. Users feel blind during long-running autonomous operations.

2. **Skills organization & MCP server UX** — The top-voted issue (#1632) demands subfolder support for skills. Combined with the MCP variable interpolation bug (#3887), there's clear frustration with the plugin/server management experience.

3. **Cost visibility and credit management** — Issue #3886 highlights that resume/restart operations consume AI credits, a design concern that touches on both fairness and transparency.

4. **Internationalization** — Issue #3883 requesting i18n support for the top 10 languages signals growing global adoption and the need for a localization framework.

5. **Extended reasoning controls** — Issue #3888 asking for independent thinking controls for Anthropic models suggests power users want finer-grained model configuration.

## Developer Pain Points

Several recurring frustrations emerge from the latest issues:

- **Authentication state loss on session resume** (#3596) — A high-impact (11 👍) bug where resuming a session breaks `/model` commands, requiring users to start fresh sessions. This undermines the session persistence feature.

- **MCP server configuration friction** — Two distinct issues (#3887 raw variable interpolation, #1579 ignored initialization instructions) indicate that MCP server integration remains brittle. Developers investing in custom MCP setups face config surprises.

- **Permission/security quirks** — Issues #2693 (`2>/dev/null` still requires permission) and #1110 (unnecessary directory access prompts) suggest the permission model is overly aggressive or inconsistent, interrupting workflow.

- **Text input scrolling** (#3885) — A seemingly minor but quality-of-life issue: long prompts cannot be scrolled within the textarea, making multi-line editing painful.

- **Lack of documentation** (#3884) — Enterprise users report that sandbox policy enforcement docs are insufficient for actual configuration using Intune/MDM.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-23

## Today's Highlights

Version 1.48.0 shipped with critical fixes for reasoning content handling and an escalation mechanism for runaway tool-call loops. Four open bugs surfaced around MCP server auto-discovery, workspace-relative tool execution, child-process hangs, and API schema compliance—all impacting production reliability. The community also proposed a new `Monitor` tool for real-time per-line streaming from background tools.

## Releases

**Version 1.48.0** | [Release](https://github.com/MoonshotAI/kimi-cli/releases/tag/1.48.0)

Changes:
- **fix(kosong): round-trip empty reasoning content** — Ensures reasoning content is preserved correctly during empty/edge-case round trips. [PR #2446](https://github.com/MoonshotAI/kimi-cli/pull/2446)
- **feat(soul): escalate repeated-tool-call reminders and force-stop on dead-end streak** — Ports kimi-code's repeated-call handling to CLI: after 3 identical tool calls, escalating reminders are injected; the turn is force-stopped when a dead-end streak is detected. [PR #2466](https://github.com/MoonshotAI/kimi-cli/pull/2466)
- Chore: version bumps for internal consistency; changelog omitted.

## Hot Issues

1. **#2457 — MCP server auto-discovers deleted config** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2457)  
   Kimi Code CLI retains and re-discovers MCP servers even after user deletion, causing persistent 400 errors that cannot be resolved. **Community reaction:** Low engagement but high severity—configuration corruption blocks all MCP workflows. Demands a "forget" or purge mechanism.

2. **#2469 — `kimi web` launches MCP servers from CLI install dir** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2469)  
   MCP tools are spawned relative to the CLI binary location, not the user's workspace. **What's at stake:** Workspace-relative MCP tools (e.g., file-scoped LSP servers) break entirely. Likely cause of #2457's duplicate config detection.

3. **#2468 — CLI hangs after detached child-process tool call** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2468)  
   Using a local mock provider with detached child processes causes indefinite hang. **Why it matters:** Blocks local development and testing with custom backends. No comments yet—may be underreported.

4. **#2465 — `kosong` sends `reasoning_effort: null` for thinking "off"** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2465)  
   OpenAILegacy provider emits `null` instead of omitting the field or sending a valid enum string. **Impact:** Violates strict OpenAI API schema; does not actually disable reasoning. Causes silent errors in production pipelines.

5. **#2453 — `kimi code` crashes on deeply nested MCP tool results** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2453)  
   Stack overflow when MCP tool returns extremely nested JSON. **Implication:** No protection against recursion depth in response parsing. Testing for adversarial/large outputs needed.

6. **#2449 — `--config` flag silently ignored for `kimi web`** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2449)  
   Users pass custom config paths but `kimi web` loads default config. **Frustration:** Config overrides are fundamental for CI/CD and multi-profile workflows; silent ignore wastes developer time.

7. **#2443 — `kimi chat` fails with `connection reset` on long context** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2443)  
   Large conversation threads (>100k tokens) cause TCP reset. **Trend:** Community seeks stability for long-running sessions; likely related to stream buffer management.

8. **#2436 — `kosong` proxy mode truncates response at 4096 chars** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2436)  
   Using kosong as an AI proxy, responses are cut at 4KB despite higher limits. **Pain point:** Surprising default truncation that breaks completion-dependent workflows.

9. **#2429 — Auth token rotation not respected by `kimi code` daemon** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2429)  
   Long-running daemon caches tokens, ignoring TTL-based rotation. **Security implication:** Potential credential staleness; forces manual restarts.

10. **#2420 — `kimi commit` generates incorrect diffs for renamed files** — [Link](https://github.com/MoonshotAI/kimi-cli/issues/2420)  
    File renames produce malformed commit diffs. **User sentiment:** Core workflow breakage for Git users; moderate upvotes indicate broad impact.

## Key PR Progress

1. **#2471 (OPEN) — `Monitor` tool for per-line stdout streaming** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2471)  
   Adds a streaming counterpart to existing background tools. Enables real-time monitoring of tool output line-by-line. **Community note:** No prior issue; pure feature proposal. Could reduce hanging (cf. #2468).

2. **#2466 (CLOSED) — Repeated-tool-call escalation** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2466)  
   Merged into 1.48.0. Addresses runaway tool loops by injecting tiered reminders and force-stopping after 3+ consecutive identical calls. Directly mitigates hangs like #2468.

3. **#2467 (CLOSED) — Release bump to 1.48.0 / kosong 0.54.0** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2467)  
   Internal version sync; changelog omitted.

4. **#2459 (OPEN) — `kosong`: add `reasoning_effort` strict mode** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2459)  
   Fixes #2465 by validating and correctly omitting `reasoning_effort` when off. **Impact:** Resolves schema compliance for strict OpenAI APIs.

5. **#2452 (OPEN) — `kimi web`: load MCP config from workspace** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2452)  
   Changes MCP server discovery to workspace-relative path. Addresses #2469 root cause.

6. **#2450 (OPEN) — `--config` flag propagation for `kimi web`** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2450)  
   Fixes the silent config ignore (#2449). Pending review.

7. **#2444 (OPEN) — Stream buffer resizing for long contexts** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2444)  
   Dynamically adjusts stream buffer to prevent `connection reset` on large conversations. Could resolve #2443.

8. **#2437 (OPEN) — `kosong`: configurable response truncation limit** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2437)  
   Makes truncation limit configurable or removes hard-coded 4096-char boundary. Addresses #2436.

9. **#2430 (OPEN) — Daemon token refresh hook** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2430)  
   Adds TTL-aware token rotation for long-running daemon mode. Fixes #2429.

10. **#2421 (OPEN) — Fix `kimi commit` diff for renamed files** — [Link](https://github.com/MoonshotAI/kimi-cli/pull/2421)  
    Corrects Git rename detection in commit generation. Directly addresses #2420.

## Feature Request Trends

- **MCP server lifecycle management** — Multiple requests for user-controlled MCP server config forget/delete (cf. #2457), workspace-relative loading (#2469), and explicit server restart/stop commands.
- **Streaming tools** — The `Monitor` tool proposal (#2471) and growing interest in real-time output from running tools suggest demand for async, non-blocking tool execution patterns.
- **Strict API schema compliance** — Issues around `reasoning_effort` (#2465), response truncation (#2436), and token formats indicate users integrating Kimi with third-party backends need strict adherence to spec.
- **Long-context reliability** — Hangs (#2468), resets (#2443), and memory issues in large sessions signal a need for better backpressure, buffering, and timeout configurability.

## Developer Pain Points

- **Configuration inconsistency** — Silent config ignores (#2449), auto-discovery after deletion (#2457), and workspace-relative path breaks (#2469) are the top recurring frustrations, eroding trust in configuration.
- **Tool execution black boxes** — Child-process hangs (#2468), near-infinite loops (#2466), and missing streaming feedback (#2471) make debugging tool calls painful. Developers want visibility and early-termination controls.
- **API compatibility gaps** — Schema violations (#2465), truncation surprises (#2436), and token rotation issues (#2429) disrupt production integrations with OpenAI-compatible backends.
- **Git integration fragility** — Broken commit diffs for renames (#2420) undermines core developer workflow trust; moderate but persistent pain across versions.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-23

## Today's Highlights
The OpenCode community is battling a memory leak regression in `opencode serve` that ballooned to 26.8 GiB on production hosts, while the team pushes forward with a major workflow engine refactor split into six reviewable PRs (part 1/6 and 2/6 now open). Plugin system architecture is evolving rapidly—a namespaced hook API landed, and a native TUI status line template system was merged after months of community demand. On the MCP front, a critical image attachment regression was closed, but the community still awaits full MCP client capabilities.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **Memory Megathread (#20695)** — 99 comments, 72 👍  
   The community's central collection point for memory issues. Core team explicitly warns against LLM-suggested solutions and requests heap snapshots. High urgency given the 26.8 GiB server-mode leak reported elsewhere.  
   [Issue #20695](https://github.com/anomalyco/opencode/issues/20695)

2. **MCP image attachment regression (#32832)** — 22 comments, 0 👍  
   Closed regression where MCP tool results containing images are lost in v1.17.5+. Community verified `1.17.4` works, `1.17.5+` broken. Minimal reproduction with standalone MCP server provided.  
   [Issue #32832](https://github.com/anomalyco/opencode/issues/32832)

3. **Full MCP client capabilities (#28567)** — 17 comments, 24 👍  
   OpenCode's MCP client is lagging behind the latest MCP 2026 standard specification. Community request for streaming, notifications, and progress support that are now standard in the protocol.  
   [Issue #28567](https://github.com/anomalyco/opencode/issues/28567)

4. **Ephemeral one-off sessions for `opencode run` (#4489)** — 12 comments, 12 👍  
   A long-standing feature request (since Nov 2025) with author offering to implement. Currently `opencode run` creates persistent sessions, which is undesirable for CI/CD or quick one-shot invocations.  
   [Issue #4489](https://github.com/anomalyco/opencode/issues/4489)

5. **Server mode memory leak to 26.8 GiB (#33213)** — 4 comments, 0 👍  
   Critical production-affecting bug: `opencode serve` accumulates anonymous JS/Bun heap, growing to 26.8 GiB cgroup peak with ~2.86 GiB swap after ~1.5 days. Restart drops to baseline instantly. Suspects JIT code retention.  
   [Issue #33213](https://github.com/anomalyco/opencode/issues/33213)

6. **TUI footer items plugin hook (#18969)** — 9 comments, 3 👍  
   Plugins currently abuse ephemeral toasts for persistent status display (token counters, TPS meters). Proposal for a `tui.footer.items` plugin hook for non-disruptive persistent status.  
   [Issue #18969](https://github.com/anomalyco/opencode/issues/18969)

7. **"Worker has been terminated" crash (#32694)** — 6 comments, 4 👍  
   Reproducible crash after first message exchange. Narrowed down: crash persists with all plugins disabled. Users must restart session after every single interaction.  
   [Issue #32694](https://github.com/anomalyco/opencode/issues/32694)

8. **MCP object parameters serialized as strings (#28472)** — 6 comments, 1 👍  
   Closed bug: MCP tools with `body` parameter of type `object` receive JSON strings instead of native objects, causing validation failures with `-32602` errors.  
   [Issue #28472](https://github.com/anomalyco/opencode/issues/28472)

9. **Tool call start time incorrectly reported (#32574)** — 6 comments, 5 👍  
   Timing block shows "start" and "end" times suspiciously close together. Codex + GPT-5.5 High triage suggests a defect in how "start" time is reset.  
   [Issue #32574](https://github.com/anomalyco/opencode/issues/32574)

10. **Plugins silently not loaded since v1.17.0 (#33455)** — 2 comments, 0 👍  
    Critical silent regression: plugins in config `plugin` array are completely absent from startup with zero logs or warnings. Affects all plugins (npm packages and local paths).  
    [Issue #33455](https://github.com/anomalyco/opencode/issues/33455)

## Key PR Progress

1. **feat(plugin): namespaced hook API (#33416)** — CLOSED  
   Replaces the v2 Effect plugin host surface with namespaced `hook` and `reload` capabilities. Adds Promise-based plugin definitions, adaptation, and scoped reconciliation. Significant plugin architecture improvement.  
   [PR #33416](https://github.com/anomalyco/opencode/pull/33416)

2. **feat(workflow): engine-core (1/6) (#32390)** — OPEN  
   First of six split-PRs from the oversized #29789. Brings modularized workflow engine with pluggable dispatcher, status machine, and trigger evaluator. Foundation for workflow automation.  
   [PR #32390](https://github.com/anomalyco/opencode/pull/32390)

3. **feat(workflow): server routes + SDK (2/6) (#32392)** — OPEN  
   Builds on engine-core PR #32390. Adds workflow HTTP API route group, handlers, and regenerated SDK client/types.  
   [PR #32392](https://github.com/anomalyco/opencode/pull/32392)

4. **feat: nested sub-agent spawning up to 5 levels (#32301)** — OPEN  
   Allows sub-agents to spawn their own sub-agents (up to 5 deep). Fixes bugs #23091 and #13715 that blocked 2→3 level transitions. Design-review proposal #32166.  
   [PR #32301](https://github.com/anomalyco/opencode/pull/32301)

5. **feat: standalone v2 session flow (#33281)** — OPEN  
   Adds `--standalone` mode running an authenticated private server child process for TUI. Creates sessions through v2 API with `DataProvider`-backed data loading.  
   [PR #33281](https://github.com/anomalyco/opencode/pull/33281)

6. **fix(tui): preserve worker rejection handling (#33448)** — CLOSED  
   Restores TUI backend worker `unhandledRejection` listener lost during Effect logging migration. Prevents Bun from terminating workers on rejected callbacks.  
   [PR #33448](https://github.com/anomalyco/opencode/pull/33448)

7. **fix(tui): scope file autocomplete to session (#33458)** — CLOSED  
   Adds reactive location context with session override. Scopes file autocomplete and mention paths to current session location. Fixes cross-project path confusion.  
   [PR #33458](https://github.com/anomalyco/opencode/pull/33458)

8. **feat(tui): native status line template system (#13885)** — CLOSED  
   Long-awaited feature (Feb 2026). Users define per-target template strings in config resolved server-side from built-in variables, shell commands, and plugin-provided data. Fixes #8619.  
   [PR #13885](https://github.com/anomalyco/opencode/pull/13885)

9. **fix(core): preserve queue after provider failure (#33460)** — OPEN  
   Distinguishes continued/completed/durably-failed provider-turn outcomes. Preserves queued work for later explicit resume. Prevents lost work on transient provider failures.  
   [PR #33460](https://github.com/anomalyco/opencode/pull/33460)

10. **feat: add --no-open flag to opencode web (#33465)** — OPEN  
    Prevents automatic browser launch when running `opencode web`. Useful for headless/CI environments.  
    [PR #33465](https://github.com/anomalyco/opencode/pull/33465)

## Feature Request Trends

- **MCP Client Modernization**: The highest-voted open feature (#28567, 24 👍) demands catching up to the latest MCP 2026 standard—streaming, notifications, and progress support. Multiple MCP-related bugs (image attachments, object serialization, fetch timeouts) underscore the community's reliance on this integration.
- **Session Management**: Two complementary requests: ephemeral one-off sessions for `opencode run` (#4489) and cross-project session pickers in TUI (#31932). Users want both lightweight disposable sessions and the ability to navigate across project boundaries.
- **Git Integration**: Two separate feature requests for native Git UI—a Git status panel for the desktop app (#15886) and a full commit/stage/push workflow (#26558). The VCS API PR (#28828) directly addresses this demand.
- **Plugin System Expansion**: Requests for persistent status display hooks (#18969) and rate limiting middleware (#33459) indicate growing sophistication in plugin usage. The namespaced hook API (#33416) is a direct response.
- **Desktop App Polish**: Direct file editing (#33017) and Chinese localization (#33467) signal that the desktop app is seeing production use and needs parity with CLI features.

## Developer Pain Points

- **Silent Configuration Failures**: Plugins silently not loading (#33455) with zero warnings is the most dangerous class of bug—developers unknowingly running without expected functionality.
- **Memory Regression in Server Mode**: The 26.8 GiB heap leak (#33213) makes `opencode serve` effectively unusable for production deployments without daily restarts. The adjacent memory megathread (#20695) suggests systemic issues.
- **Crash-on-First-Message**: The "Worker has been terminated" bug (#32694) affecting every conversation makes the tool completely unusable for those impacted, even with all plugins disabled.
- **MCP Ecosystem Fragility**: Multiple MCP regressions (image attachments, object serialization, hardcoded fetch timeouts) damage trust in a core integration point. The community clearly relies on MCP tools heavily.
- **Post-Migration Data Loss**: Pre-migration sessions stranded after the event-sourcing migration (#33447)—data exists in legacy tables but is invisible and unresumable. For users with months of session history, this is a significant workflow disruption.
- **Cross-Project UX Gaps**: The session picker being scoped to the current project (#31932) and stale project roots after directory moves (#30685) show that multi-repo workflows remain painful.
- **Billing Confusion**: A subscription renewal bug (#33451)—payments going to Zen balance instead of renewing Go subscription—indicates potential issues in the billing integration that could affect user trust in paid tiers.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-23

## Today's Highlights
Release v0.79.10 shipped with a key extension API improvement, adding compaction reason context to session lifecycle events — a direct response to community feedback on missing observability. Meanwhile, the project is actively addressing a cluster of "hang" and "stuck on Working..." bugs affecting multiple LLM providers, with OpenAI Codex reliability (#4945) and general agent-loop deadlocks (#5778) receiving sustained developer attention. A flurry of new provider integrations (Merge Gateway, Anthropic Vertex, Neuralwatt) signals continued expansion of the ecosystem.

## Releases
**v0.79.10** — [Release](https://github.com/badlogic/pi-mono/releases/tag/v0.79.10)
- **Extension compaction event context**: `session_before_compact` and `session_compact` events now include `reason` (`"manual" | "threshold" | "overflow"`) and `willRetry`, enabling extensions to distinguish manual `/compact` from auto-compaction and overflow retry flows. Closes multiple related issues including #5217.

---

## Hot Issues

1. **[#4945] openai-codex Connection Reliability Issues** — [Issue](https://github.com/earendil-works/pi/issues/4945)  
   *64 comments, 30 👍*  
   Users report OpenAI Codex/gpt-5.5 sessions freezing on "Working..." with no streamed output, tool calls, or errors. Only recovery is pressing Escape. Ongoing for a month; high community impact as Codex is a primary provider.

2. **[#3357] Official local LLM provider extension** — [Issue](https://github.com/earendil-works/pi/issues/3357)  
   *27 comments, 36 👍*  
   Request to dynamically fetch model lists from `{baseUrl}/models`, making Pi work seamlessly with llama.cpp, Ollama, LM Studio. Highly upvoted; seen as critical for offline/local-first workflows.

3. **[#5653] Move off Shrinkwrap** — [Issue](https://github.com/earendil-works/pi/issues/5653)  
   *15 comments*  
   Duplicate copies of `pi-ai` on disk when both `pi-ai` and `pi-coding-agent` are installed, causing provider registry splits because API registries are module-level Maps. Core packaging problem affecting multi-tool setups.

4. **[#5916] Support provider extensions with model aliases and improve search** — [Issue](https://github.com/earendil-works/pi/issues/5916)  
   *11 comments*  
   No UI for OpenRouter provider configuration; users resort to manual `models.json` overrides. Request for better provider search and alias support, reflecting friction in multi-provider setups.

5. **[#5778] pi-agent-core hangs indefinitely on unresponsive streams or tool execution deadlocks** — [Issue](https://github.com/earendil-works/pi/issues/5778)  
   *8 comments*  
   Critical vulnerability: agent loop wedges if LLM stream drops without closing iterator, or if a tool's `execute()` promise never resolves. Foundation of several "Working..." hang scenarios.

6. **[#5291] Sessions hang on "working" when used with Anthropic subscription** — [Issue](https://github.com/earendil-works/pi/issues/5291)  
   *6 comments, 2 👍*  
   Users with Anthropic Enterprise subscriptions experience simultaneous session freezes. Interrupt/stop sometimes works, sometimes requires waiting. Suggests rate-limit or credential rotation issues.

7. **[#4748] pi-tui: `getKeybindings()` realm/instance singleton breaks extensions** — [Issue](https://github.com/earendil-works/pi/issues/4748)  
   *5 comments, 2 👍*  
   Module-scope singleton in keybindings.ts means extensions loaded from different `node_modules` paths see distinct instances — extensions from `pi-coding-agent` can't read keybindings set by Pi.

8. **[#5871] Anthropic OAuth-token detection is hardcoded to sk-ant-oat** — [Issue](https://github.com/earendil-works/pi/issues/5871)  
   *4 comments*  
   Anthropic provider hardcodes `"sk-ant-oat"` substring check for OAuth detection, preventing custom OAuth credentials. PR #5977 addresses this with explicit `authMode`.

9. **[#5263] Make in-session model and thinking-level changes ephemeral by default** — [Issue](https://github.com/earendil-works/pi/issues/5263)  
   *4 comments, 4 👍*  
   Currently `/model` changes the global `defaultModel` setting silently (#5976 confirms this). Request to limit in-session changes to the active session only, with a dedicated settings UI for defaults.

10. **[#5810] RPC: expose session entries and tree** — [Issue](https://github.com/earendil-works/pi/issues/5810)  
    *3 comments*  
    Request for read-only RPC commands (`get_entries`, `get_tree`) so external tools and scripts can inspect session state. Indicates growing demand for programmatic Pi integration.

---

## Key PR Progress

1. **[#5526] Require terminal events for OpenAI Responses streams** — [PR](https://github.com/earendil-works/pi/pull/5526)  
   Fixes OpenAI responses randomly stopping mid-generation and context counters getting desynchronized. Ensures streams end with a terminal response event before accepting completion.

2. **[#5987] fix(coding-agent): resolve --session by agent name via identity daemon** — [PR](https://github.com/earendil-works/pi/pull/5987)  
   Pi now queries the identity daemon when `--session` receives an agent name (e.g. `lucid-gecko-24`), resolving to the correct session file path. Closes a gap between extension and core.

3. **[#5859] fix(ai): send responses prompts as instructions** — [PR](https://github.com/earendil-works/pi/pull/5859)  
   OpenAI Responses APIs expect system prompts in top-level `instructions`, not replayed `input` messages. Fixes compatibility for Azure OpenAI and Codex Responses.

4. **[#5985] feat(ai): add Merge Gateway provider** — [PR](https://github.com/earendil-works/pi/pull/5985)  
   New built-in provider (`merge-gateway`) authenticated via `MERGE_GATEWAY_API_KEY`, giving access to 40+ models from a single API key. Mirrors existing provider patterns.

5. **[#5981] Linkify plain URLs in Text output** — [PR](https://github.com/earendil-works/pi/pull/5981)  
   Auto-links plain HTTP(S) URLs rendered by `Text` using OSC 8 hyperlinks when terminal supports it. Fixes long OAuth URLs (like MCP auth) being unclickable after wrapping.

6. **[#5977] feat(ai): allow explicit authMode overrides for Anthropic provider** — [PR](https://github.com/earendil-works/pi/pull/5977)  
   Introduces `authMode` compatibility flag so providers/models can explicitly declare OAuth/Bearer credentials, replacing the hardcoded `"sk-ant-oat"` heuristic. Addresses #5871.

7. **[#5262] feat(ai): add Anthropic Vertex provider** — [PR](https://github.com/earendil-works/pi/pull/5262)  
   Adds `anthropic-vertex` provider for Claude on Google Cloud Vertex AI. Thin adapter using existing Anthropic Messages streaming path. Important for GCP users.

8. **[#5970] feat: add auto-router extension for DeepSeek V4 Pro/Flash** — [PR](https://github.com/earendil-works/pi/pull/5970)  
   Extension that routes between DeepSeek V4 Flash (simple tasks) and V4 Pro (complex tasks) based on prompt complexity analysis. Claims 60-70% cost savings.

9. **[#5963] fix(ai): reject malformed final tool call arguments** — [PR](https://github.com/earendil-works/pi/pull/5963)  
   Validates final streamed tool-call argument JSON before `toolcall_end`/`done`, failing with `stopReason: "error"` instead of exposing malformed arguments. Prevents silent tool failures.

10. **[#5955] fix(coding-agent): add secret-disclosure scope discipline to default system prompt** — [PR](https://github.com/earendil-works/pi/pull/5955)  
    Prevents Pi from sweeping secrets into destinations during broad file copy tasks. Ensures Pi correctly identifies safe subsets without freezing on disclosure rules.

---

## Feature Request Trends

The community is converging on several clear feature directions:

- **Dynamic provider configuration**: Multiple requests (#3357, #5916, #5965) ask for runtime model list fetching from provider base URLs, better provider aliasing, and clearer UI labels — the ecosystem is outgrowing static configuration.
- **Ephemeral session settings**: Issues #5263 and #5976 highlight strong demand for in-session model/thinking changes to remain local to the session, not silently overwrite global defaults.
- **Programmatic session access**: #5810 and #5932 request RPC endpoints and extension APIs for inspecting session state, entry trees, and navigation — users want to build custom tools (e.g., `/goal` implementations) on top of Pi.
- **New provider integrations**: PRs for Merge Gateway, Anthropic Vertex, auto-routing, and Neuralwatt (#5985, #5262, #5970, #5914) show the community actively expanding the provider surface.

---

## Developer Pain Points

- **"Working..." hang / indefinite stalls**: The single largest pain point spans multiple providers (OpenAI Codex #4945, Anthropic #5291, general agent loop #5778). Underlying causes include missing stream termination, unclosed iterators, unresponsive tool execution, and WebSocket timeout handling.
- **Packaging and modularity friction**: Duplicate module instances (#5653, #4748) caused by npm hoisting patterns break singleton registries and keybinding state — a recurring theme as the project grows its extension ecosystem.
- **Hardcoded provider assumptions**: Anthropic's OAuth detection (#5871) and Amazon Bedrock's missing inference profile IDs (#3704) force users into provider-specific workarounds rather than uniform configuration.
- **Silent global state mutation**: The `/model` command unexpectedly overwrites `defaultModel` settings (#5976), and tool argument validation failures can produce empty error messages (#2188) — both erode developer confidence in predictable behavior.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-23

## Today's Highlights

The Qwen Code repository saw a burst of community activity today, with **50+ issues and 50+ PRs** updated in the last 24 hours. A major wave of **input validation fixes** from contributor `tt-a1i` (20+ PRs on integer/range boundary issues) has drawn both attention and pushback—prompting a new maintainer PR to add batch-detection guards against "validation noise." Meanwhile, two **release workflows failed**, **6 new bugs** related to fractional-value acceptance were filed, and the **wizard UI for custom providers** continues to be a top community pain point.

## Releases

No new releases in the last 24 hours. The most recent tags `v0.19.0-preview.0` and `v0.18.5-nightly.20260623` both failed their `integration_none` jobs (Issues [#5686](https://github.com/QwenLM/qwen-code/issues/5686) and [#5725](https://github.com/QwenLM/qwen-code/issues/5725)).

## Hot Issues

1. **#5090** — [CLOSED] *Refactor: Decouple Provider Identity from SDK Protocol*  
   Proposed making `providerId` a free-form string with a new `Protocol` enum (`OPENAI | GEMINI | ANTHROPIC | QWEN_OAUTH`). High comment activity (6) despite being closed; signals strong community desire for flexible provider routing.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5090)

2. **#3877** — *bug: qwen code raise missing API key error although .env file contain OPENCODE_GO_API_KEY*  
   Long-standing (opened May 6) with 5 comments. Users report `.env` files in `~/.qwen/` are ignored on startup. Core UX friction for new users.  
   [Link](https://github.com/QwenLM/qwen-code/issues/3877)

3. **#5708** — *bug(cli): session list cursor accepts negative and unsafe values*  
   Part of today's validation wave. Cursor values that are finite but invalid (not valid `mtimeMs` values) pass through. Affects both REST and ACP HTTP endpoints.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5708)

4. **#5656** — *Move tool-use summaries from conversation history to the loading indicator*  
   UX request: tool-use labels (e.g., "Fixed NPE in UserService") currently clutter conversation history; should move to loading indicator area.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5656)

5. **#4814** — [CLOSED] *UI should make it easier for Custom Provider users to add new models*  
   Wizard flow only shows a text field for custom models after initial provider selection; users want a dedicated "Add Model" button post-setup.  
   [Link](https://github.com/QwenLM/qwen-code/issues/4814)

6. **#5713** — *semi-invisible cursor in Alacritty*  
   Cursor rendering broken on Alacritty terminal (OK in Xterm). Affects Linux users of a popular terminal emulator.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5713)

7. **#5634** — *autofix tier-1 trusts an LLM-applied ready-for-agent label*  
   Security concern: a bot-applied label (`status/ready-for-agent`) can be influenced by untrusted issue text, potentially bypassing human-engagement filters in CI/CD.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5634)

8. **#5641** — *Qwen Code repeats completed shell tool results on current npm latest*  
   Deterministic bug: a completed shell tool result is re-submitted after being returned. Includes a standalone reproducer against the public npm package.  
   [Link](https://github.com/QwenLM/qwen-code/issues/5641)

9. **#5611** — *web_fetch can't fetch JSON APIs — HTTP 415*  
   `web_fetch` only sends `text/*` Accept headers, blocking JSON REST API calls (e.g., GitHub API).  
   [Link](https://github.com/QwenLM/qwen-code/issues/5611)

10. **#5722** — *Token speed display bugs: tok/s disappears during thinking, stalls during tool calls, inaccurate values*  
    Three specific TUI rendering bugs in the token-per-second display, affecting reasoning models and tool-call workflows.  
    [Link](https://github.com/QwenLM/qwen-code/issues/5722)

## Key PR Progress

1. **#5729** — *fix(core): keep active runtime model in default getAllConfiguredModels listing*  
   Fixes regression where an active model's `authType` is dropped from the default listing. Core fix for model visibility.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5729)

2. **#5730** — *feat(desktop): show file preview in a resizable side panel instead of fullscreen*  
   UX improvement for the desktop app: replaces fullscreen file overlays with a docked resizable panel.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5730)

3. **#5727** — *docs: add vertex-ai auth, missing commands, and qc-helper index entries*  
   Audit fixing documentation drift in 6 files; `vertex-ai` auth type was entirely undocumented despite existing in code.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5727)

4. **#5638** — *fix(daemon): Refresh workspace provider defaults*  
   Makes `GET /workspace/providers` build snapshot daemon-side from fresh workspace settings each request, removing stale cache dependency.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5638)

5. **#5589** — *docs: Align docs with current CLI behavior*  
   Refreshes user/developer docs for MCP management, extension settings, themes, sandbox links, SDK permissions, and Qwen OAuth status.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5589)

6. **#5654** — *fix(cli): restore saved custom model IDs when re-entering the auth wizard*  
   Pre-fills custom model IDs on wizard re-entry instead of resetting to provider defaults. Directly addresses #4814-style pain.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5654)

7. **#5245** — *fix: hide empty native sessions on Windows*  
   Two Windows fixes: expands `~\` paths to home directory, hides phantom `(session)` entries from the session list.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5245)

8. **#5723** — *fix(triage): strengthen PR gate with batch detection, problem existence check, and red flag patterns*  
   Maintainer response to `tt-a1i`'s 20-PR day: adds batch-detection logic to prevent validation-noise PRs from overwhelming reviewers.  
   [Link](https://github.com/QwenLM/qwen-code/pull/5723)

9. **#4653** — *feat(core): respect configurable agent ignore files*  
   Adds support for `.agentignore` and `.aiignore` alongside `.qwenignore`, plus a `context.ignoreFiles` config option. Long-running PR (since May 31).  
   [Link](https://github.com/QwenLM/qwen-code/pull/4653)

10. **#5666** — *docs(tui): design for Ctrl+O transcript view, removing compact mode*  
    Design-first PR replacing the `compactMode` toggle with a dedicated Ctrl+O transcript view (alternate screen buffer). Claude Code-like UX alignment.  
    [Link](https://github.com/QwenLM/qwen-code/pull/5666)

## Feature Request Trends

- **Custom Provider UX** (#4814, #5090): Strong demand for easier model management in custom/provider setups—wizard pre-fills on re-entry, dedicated "Add Model" buttons, free-form provider IDs.
- **Terminal UX Enhancement** (#5656, #5666): Users want cleaner conversation history—tool-use summaries moved to loading indicators, compact mode replaced with a dedicated transcript view.
- **Tool Capability Expansion** (#5611): `web_fetch` needs to support JSON APIs, not just text/html. A clear gap for developer-facing workflows.
- **Desktop File Preview** (#5730): Side-panel previews instead of fullscreen overlays—polish for the desktop app.
- **Ignore File Configuration** (#4653): Community wants multi-tool ignore files (`.agentignore`, `.aiignore`) with configurable paths.

## Developer Pain Points

- **Input Validation Gaps**: 11+ issues today alone on fractional/negative/zero values being accepted where integers are required—cursors, limits, timeouts, connection counts. This was the single largest category of community noise.
- **Environment Variable Handling** (#3877): `.env` files in `~/.qwen/` being ignored on startup is a persistent onboarding friction point (open since May 6).
- **Token Display Bugs** (#5722): The tok/s UI has three distinct bugs (disappears during thinking, stalls during tool calls, inaccurate values)—a significant trust/reliability concern for users monitoring costs.
- **Release Pipeline Reliability** (#5686, #5725): Two sequential release versions failed at the same `integration_none` stage, suggesting a systemic CI issue affecting both preview and nightly builds.
- **CI/CD Security** (#5634): The autofix pipeline's trust of an LLM-applied label that can be influenced by issue text raised valid security concerns about automated workflow hijacking.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI / CodeWhale Community Digest
**Date: 2026-06-23**

---

## Today's Highlights

The project continues its extensive **v0.8.65 provider-scoped routing overhaul** with a burst of activity today: **10 PRs** landed addressing provider onboarding, route validation, and model-scoping. Critical regression fixes landed for **Together AI DeepSeek routes** and **Baidu Qianfan** integration, while the maintainer pushed forward the **Fleet execution substrate** and **provider-scoped model picker** initiatives. The community is actively contributing provider fixtures for Chinese cloud vendors, with Xiaomi MiMo, Alibaba Bailian, and SiliconFlow all receiving dedicated PRs.

---

## Releases

- **v0.8.64** (CodeWhale): Released as a security and release integration milestone. This is the canonical release name; the legacy `deepseek-tui` npm package is deprecated with no further releases. Users on v0.8.x should migrate per `docs/REBRAND.md`.

---

## Hot Issues

1. **#2942 – [CLOSED] CodeWhale自问自答 (self-answering)**  
   `shadowjer` reported the tool executing uncommanded actions, corrupting projects. **Closed** after 7 comments; likely tied to tool-call over-eagerness fixes in v0.8.64.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/2942)

2. **#1978 – OpenRouter-compatible base_url fixture**  
   `nbiish`'s 6-comment issue pushes for custom base URL support using ZenMux as concrete fixture. Core to the provider-scoped routing architecture.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/1978)

3. **#3222 – Inline thinking blocks rendering**  
   `buko` reports OpenAI-compatible gateways emitting `<think>...</think>` blocks aren't displayed correctly. 6 comments, patch direction accepted.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3222)

4. **#2621 – Xiaomi MiMo Token Plan integration**  
   `springeye` pushes for full mode support: endpoint/auth, model availability, quota display, and rate-limit behavior. 5 comments; partial endpoint/auth work landed.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/2621)

5. **#3289 – Fleet worker fanout freeze regression**  
   `bruce6135` reports TUI freezes when spawning multiple Fleet/subagent workers. 5 comments, needs current build proof of resilience.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3289)

6. **#3405 – Provider/model setup wizard**  
   Maintainer-driven issue: highest-friction first-run path needs a provider/model step leveraging v0.8.65 cleanup. 1 comment, active development.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3405)

7. **#3019 – Codex/Responses route reliability**  
   Maintainer `Hmbown` targets retry/backoff parity, tool-result serialization, and usage metadata for the OpenAI Codex/Responses route. 3 comments, foundational for agent workflows.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3019)

8. **#3357 – Baidu Qianfan custom provider route**  
   `CaiWeibo` reports model not working with tools; requests `--provider` custom option for URL/API key/model name. 2 comments, fast-tracked.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3357)

9. **#3320 – Alibaba Bailian API key onboarding**  
   `maomaochong998` reports missing Aliyun Bailian API key integration. 2 comments, architecture contract aligned with #1519/#2608/#3084.  
   [View Issue](https://github.com/Hmbown/CodeWhale/issues/3320)

10. **#3382 – Together DeepSeek route validation failure**  
    Observed June 22: model `deepseek-ai/DeepSeek-V4-Pro` rejected as "DeepSeek model" on Together provider. 1 comment, fix landed today.  
    [View Issue](https://github.com/Hmbown/CodeWhale/issues/3382)

---

## Key PR Progress

1. **#3429 – Xiaomi MiMo catalog evidence**  
   Adds current Token Plan model-summary evidence captures. Updates static metadata for `mimo-v2.5-pro-ultraspeed` at 1M context window.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3429)

2. **#3428 – Scope model candidates to active provider**  
   Core fix for #3383: `/model` surfaces are now provider-scoped by default. Removes cross-provider implicit switching from bare model strings.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3428)

3. **#3427 – SiliconFlow TokenHub route diagnostics**  
   Preserves #2629 as regression fixture. Proves `siliconflow-CN` stays first-class, TokenHub uses `[providers.openai]` with `deepseek-ai/DeepSeek-V4-Pro`.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3427)

4. **#3426 – Accept Together-owned DeepSeek routes**  
   Allows Together provider to validate DeepSeek V4 Pro and Flash wire IDs. Adds Flash completion/default mapping.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3426)

5. **#3425 – Baidu Qianfan route fixture**  
   Adds first-class OpenAI-compatible provider descriptor with `qianfan`/`baidu-qianfan` aliases. Wires `QIANFAN_API_KEY`, `QIANFAN_BASE_URL`, `QIANFAN_MODEL` env sources.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3425)

6. **#3424 – DashScope OpenAI-compatible fixture**  
   Documents Alibaba Bailian/Model Studio DashScope as explicit OpenAI-compatible route with regional `compatible-mode/v1` base URL and `qwen-plus`.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3424)

7. **#3423 – OpenRouter-compatible base URLs documentation**  
   Finishes #1978 validation/docs slice. Documents `provider = "openrouter"` + `[providers.openrouter].base_url` shape.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3423)

8. **#3422 – Codex Responses retry edge coverage**  
   Generalizes retry test helper beyond 429s. Adds transient 503 regression proving `handle_responses_stream` retries through service unavailability.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3422)

9. **#3327 – First-class sub-agent toggle**  
   Adds `/config subagents on|off|status` plus `/config features.subagents true|false` as runtime toggle for subagents. Session-only changes via `AppAction::UpdateFeatures`.  
   [View PR](https://github.com/Hmbown/CodeWhale/pull/3327)

10. **#3370 – WeCom (企业微信) intelligent robot bridge**  
    Community contribution (`pkeging`) adding WeCom enterprise WeChat integration bridge. New integration surface.  
    [View PR](https://github.com/Hmbown/CodeWhale/pull/3370)

---

## Feature Request Trends

- **Multi-provider routing architecture** – Dominant theme: provider-scoped routing, fallback chains, route metadata, and explicit switching. Users want to mix DeepSeek, OpenAI, Alibaba, Baidu, Xiaomi, and local models without implicit provider switching.
- **Fleet execution substrate** – Emerging pattern: profiled worker execution, agent roles/loadouts/permissions, and semantic model routing. Multiple EPICs (#3154, #3167, #3205) targeting v0.8.65.
- **Provider onboarding wizards** – Setup flow is the top friction point. Requests for interactive provider/model selection with health checks, API key managers, and catalog browsers.
- **Secret management** – Users want provider-scoped API keys from external commands/secret managers, not stored in config files or shell history (#3004).
- **Synthesis/reduce pass** – WhaleFlow swarm pattern wants a reduce stage to combine multiple worker outputs into coherent results (#3230).

---

## Developer Pain Points

- **Provider/model configuration complexity** – Highest-frequency complaint. Users struggle with mixing provider identity, model identity, and wire protocol IDs. The project is actively disentangling these (#2608).
- **Implicit cross-provider switching** – Model strings silently changing providers is a recurring source of bugs and confusion (#3382, #3383).
- **Tool-call reliability** – Stream parsing failures (DSML tool-call markup streaming as text, #2900), premature completion states (#2989), and tool-call over-eagerness (#2942) persist despite progress.
- **TUI freeze under load** – Spawning multiple Fleet/subagent workers can freeze input/render/cancel (#3289). High-impact for agent workflows.
- **Chinese cloud provider onboarding** – Multiple reports (SiliconFlow, Alibaba Bailian, Baidu Qianfan, Xiaomi MiMo) of missing API key integration, base URL configuration, and model discovery. Community is actively contributing fixtures, but the onboarding path remains fragmented.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*