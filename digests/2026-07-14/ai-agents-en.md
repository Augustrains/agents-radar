# OpenClaw Ecosystem Digest 2026-07-14

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-14 01:13 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-07-14

## 1. Today's Overview

OpenClaw shows intense development activity with **500 issues and 500 PRs updated in the last 24 hours**, reflecting a large, actively maintained open-source project. The project released **v2026.7.1 (stable) and v2026.7.1-beta.6** today, featuring new AI model providers and default model changes. Critical stability concerns persist with **two P0 regressions** — tool results returning placeholder strings and session initialization conflicts — both actively discussed in the community. The project remains in a high-velocity cycle with substantial community engagement (112 comments on the long-standing Linux/Windows app request), but several high-severity bugs remain open awaiting maintainer review.

---

## 2. Releases

### v2026.7.1 (Stable)
- **New providers**: Added Featherless, Claude Sonnet 5, Mythos 5, Meta Muse Spark 1.1, and ClawRouter
- **Default model change**: GPT-5.6 is now the default for new setups
- **Think modes**: `/think ultra` for Sol and Terra, `max` for Luna
- **Z.AI support**: Honors Z.AI `max` mode
- **OAuth improvement**: Model availability refreshes after OAuth authentication

### v2026.7.1-beta.6
- Identical changelog to stable release — appears to be a pre-release candidate

**No breaking changes or migration notes documented in the release artifacts.**

---

## 3. Project Progress

Today's activity shows significant closure velocity:

### Recently Closed Issues (245 merged/closed PRs, 193 closed issues)
- **Codex runtime compatibility** — #103884 ([link](openclaw/openclaw Issue #103884)): GPT-5.6 Sol now works in OpenClaw's Codex runtime
- **Session initialization conflict** — #102400 ([link](openclaw/openclaw Issue #102400)): Slack/webchat/heartbeat channels now handle retry properly
- **Codex metadata registration** — #106140 ([link](openclaw/openclaw Issue #106140)): Fixed runtime state dereference crash
- **Gateway security** — #105936 ([link](openclaw/openclaw Issue #105936)): fs.listDir pairing now properly requires `operator.admin`
- **Refactoring momentum** — #106503, #106555 ([link](openclaw/openclaw Issue #106503), [link](openclaw/openclaw Issue #106555)): Runtime modules being split from 4,000+ line monoliths

### Notable Open PRs Under Active Development
- **Event-loop stall fix** — #89040 ([link](openclaw/openclaw PR #89040)): XL-sized perf fix for `embedded_run` bootstrap (P1, ready for proof)
- **Reply-session self-heal** — #101920 ([link](openclaw/openclaw PR #101920)): Automatically recovers from reply-session init conflicts instead of permanent session wedging (P1)
- **Subagent progress on Discord** — #95604 ([link](openclaw/openclaw PR #95604)): Aims to give Discord users visible subagent activity feedback (XL, ready for maintainer look)
- **Codex catalog continue** — #106927 ([link](openclaw/openclaw PR #106927)): New feature enabling paired-node Codex session continuation from Control UI (XL, maintainer-authored)

---

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Summary |
|----------|----------|-----------|---------|
| **#75** ([link](openclaw/openclaw Issue #75)) | 112 | 👍 81 | **Linux/Windows Clawdbot Apps** — The most-engaged issue by far. Community strongly desires desktop apps for non-Apple platforms. Stale since January 2026; labeled `P2` with multiple `clawsweeper` review tags. |
| **#7707** ([link](openclaw/openclaw Issue #7707)) | 18 | 👍 0 | **Memory Trust Tagging** — Feature request to tag agent memories by source trust level. Open since February, unresolved. Multiple security labels. |
| **#104721** ([link](openclaw/openclaw Issue #104721)) | 16 | 👍 1 | **P0 regression: "(see attached image)" placeholder** — The most critical bug today. Users report complete loss of tool output — literal placeholder strings replace actual data. |
| **#102020** ([link](openclaw/openclaw Issue #102020)) | 13 | 👍 1 | **Session init conflict on second message** — Cross-channel bug affects Signal and other platforms. Second message in any session fails. |
| **#38327** ([link](openclaw/openclaw Issue #38327)) | 11 | 👍 3 | **"Cannot convert undefined or null to object"** — P1 regression affecting Google Vertex/Gemini users after update to 2026.3.2. |
| **#101290** ([link](openclaw/openclaw Issue #101290)) | 11 | 👍 1 | **Database corruption on macOS** — P0 SQLite state corruption during CLI startup while gateway runs. Only reproduces on macOS. |

**Community Sentiment Analysis**: The highest-signal topics reveal three dominant needs:
1. **Cross-platform support** (Issue #75) — users feel macOS/iOS are prioritized over Windows/Linux
2. **Reliability anxiety** — multiple P0 regressions in the stable release track eroding trust
3. **Security awareness** — multiple feature requests for trust tagging, sandboxing, and denylist controls

---

## 5. Bugs & Stability

### P0 (Critical) — Active, No Fix PR Yet
- **#104721** ([link](openclaw/openclaw Issue #104721)): All tool results return literal `"(see attached image)"` string instead of actual output. **Stable release blocker** labeled. Reported 2026-07-11, still open.
- **#101290** ([link](openclaw/openclaw Issue #101290)): CLI startup preflight corrupts SQLite state while gateway runs on macOS — `"database disk image is malformed"`. Four occurrences in five days.

### P1 (High) — Active
- **#102020** ([link](openclaw/openclaw Issue #102020)): Second message fails with "reply session initialization conflicted" across Signal and Discord. **Fix PR #101920** ([link](openclaw/openclaw PR #101920)) open — adds self-healing logic.
- **#38327** ([link](openclaw/openclaw Issue #38327)): Google Vertex/Gemini 3.1 "Cannot convert undefined or null to object" — P1 regression since 2026.3.2.
- **#100121** ([link](openclaw/openclaw Issue #100121)): Exec/tool failures suppress model response, show "(see attached image)" — related to #104721 but separate root cause (3 interacting code paths).
- **#103076** ([link](openclaw/openclaw Issue #103076)): Legacy state migration still blocks gateway startup after partial fix — 5 more migration sources remain.
- **#90944** ([link](openclaw/openclaw Issue #90944)): `sessions_yield` reply recorded but not delivered — user gets child summary instead of parent reply.

### Fix PRs Available
- **#106851** ([link](openclaw/openclaw PR #106851)): Fixes retry classifier for provider-wrapped 5xx errors — addresses #106824
- **#105323** ([link](openclaw/openclaw PR #105323)): Memory pressure guard for large base64 image decoding
- **#106464** ([link](openclaw/openclaw PR #106464)): Null tool parameters workaround for strict providers like DeepSeek
- **#106932** ([link](openclaw/openclaw PR #106932)): Prevents parent Codex binding retirement when creating detached dashboard child (fixes #106778)

### Regression Pattern
Three separate regressions (April–July 2026) involve tool output being replaced with placeholder strings, suggesting a systemic issue in output rendering/tool result plumbing.

---

## 6. Feature Requests & Roadmap Signals

### High-Community-Interest Features
| Issue | Votes | Summary | Likely Next Version? |
|-------|-------|---------|---------------------|
| **#75** ([link](openclaw/openclaw Issue #75)) | 81 👍 | Linux/Windows desktop apps | **Unlikely** — stale since Jan 2026, no PR activity, labeled `clawsweeper:needs-product-decision` |
| **#6615** ([link](openclaw/openclaw Issue #6615)) | 7 👍 | Denylist support for exec-approvals | **Possible** — complements existing allowlist, multiple security labels |
| **#7722** ([link](openclaw/openclaw Issue #7722)) | 4 👍 | Filesystem sandboxing config | **Possible** — aligns with recent security PRs (#105936, #100953) |
| **#7707** ([link](openclaw/openclaw Issue #7707)) | 0 👍 | Memory trust tagging by source | **Unlikely** — low reaction count, complex security feature |
| **#10118** ([link](openclaw/openclaw Issue #10118)) | 4 👍 | TUI Shift+Enter for newline | **Likely** — simple UX improvement, labeled TUI |

### Roadmap Indicators from Recent PRs
- **Codex integration deepening** — PR #106927 (Codex catalog sessions in Control UI) signals continued investment
- **Security hardening** — Multiple security-focused PRs (image size guards, plugin audit warnings, Vault response bounds) suggest a security improvement cycle
- **Multi-agent UX** — PR #95604 (Discord subagent progress) and #95996 (parent yield fixes) show focus on subagent orchestration

**Predictions for v2026.8.x**: TUI Shift+Enter support, improved subagent progress visualization, expanded denylist controls, and fixes for the remaining Codex OAuth issues.

---

## 7. User Feedback Summary

### Pain Points (Negative Signals)
- **"Completely broken"** — User describing #104721 (tool output regression) — strong language indicating frustration with stability
- **"Silently lost"** — LINE channel message loss (#86012) — users unaware of failures
- **"Permanently wedged"** — Session conflict bugs causing irreversible state corruption (#98790)
- **Database corruption** — macOS users reporting `"database disk image is malformed"` on stable release (#101290)
- **Need for production stability labels** — #73537: Family/business user requests clearer stability indicators

### Satisfaction Signals (Positive Indicators)
- **High engagement with maintainers** — 112 comments on Issue #75 shows community cares deeply about the project
- **"Genuinely become part of our daily workflow"** — User quote from Issue #73537, despite frustration
- **Quick closure of security issues** — #105936 closed same-day (fs.listDir authorization fix)
- **Active bug triage** — Multiple regression reports receiving maintainer labels within hours

### Notable Use Cases
- Family and business assistant (Telegram integration, automations, cron jobs, Home Assistant)
- Multi-agent setups with inter-agent traffic via `sessions_send`
- Local-first personal assistant with cross-context operation
- Codex CLI integration for developer workflows

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention (Long-Standing + High Impact)

| Issue | Age | Last Update | Priority | Summary |
|-------|-----|-------------|----------|---------|
| **#75** ([link](openclaw/openclaw Issue #75)) | 195 days | 2026-07-13 | P2 | Linux/Windows apps — 112 comments, 81 👍, multiple maintainer-review labels, no product decision |
| **#6615** ([link](openclaw/openclaw Issue #6615)) | 163 days | 2026-07-13 | P2 | Exec-approval denylist — 7 👍, security review needed, labeled `fix-shape-clear` |
| **#10687** ([link](openclaw/openclaw Issue #10687)) | 158 days | 2026-07-13 | P2 | Dynamic model discovery — stale since Feb, needs live reproduction |
| **#9986** ([link](openclaw/openclaw Issue #9986)) | 158 days | 2026-07-14 | P2 | Model fallback on context exceeded — basic reliability feature |
| **#50291** ([link](openclaw/openclaw Issue #50291)) | 117 days | 2026-07-13 | P2 | Plugin trace context — missing observability fields for distributed tracing |

### Stale PRs Requiring Attention
- **#89040** ([link](openclaw/openclaw PR #89040)): Event-loop stall fix — P1, opened 43 days ago, still "needs proof"
- **#103290** ([link](openclaw/openclaw PR #103290)): Hermes import retry — P0, opened 4 days ago, unranked rating, needs proof
- **#106339** ([link](openclaw/openclaw PR #106339)): JSON5 comment preservation — P0, opened yesterday, ready for maintainer look — critical UX issue with config persistence

### Systemic Concerns
- **4 of the top-10 most-commented issues** carry `clawsweeper:needs-product-decision` labels, suggesting product direction bottlenecks
- Multiple P0/P1 regressions remain open with `clawsweeper:no-new-fix-pr` tags, indicating the maintainers may be prioritizing feature work over bug fixes
- The `clawsweeper:needs-live-repro` tag on 7 of the top issues suggests difficulty reproducing complex cross-platform bugs

---

**Project Health Assessment**: 🟡 *Cautious* — Strong community engagement and release velocity, but multiple P0 regressions on the stable track and a growing backlog of product decisions create risk. The maintainers appear to be balancing rapid feature development (Codex integration, new providers) with necessary stability work. Users should evaluate v2026.7.1 carefully before production deployment due to the open tool-output regression.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report for the AI agent open-source ecosystem as of **July 14, 2026**.

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is in a period of **intense, high-velocity maturation**. The major projects are no longer proving viability but are fighting a war of attrition against **stability regressions** — particularly around tool-call management, session state integrity, and multi-provider support. A clear bifurcation is emerging: **mega-projects** (OpenClaw, IronClaw) are refactoring monolithic codebases into extensible architectures, while **focused tools** (NanoBot, PicoClaw) are shipping targeted features like webhooks and localization. The community is pushing back against feature bloat and instability, demanding cross-platform support, deterministic pipeline control, and granular security. The ecosystem as a whole is highly responsive but faces a growing backlog of product decisions and architectural governance questions.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Today | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 500 🟢 | 500 🟢 | v2026.7.1 (Stable) | 🟡 Cautious |
| **NanoBot** | 13 🟡 | 45 🟢 | None | 🟢 Healthy |
| **Hermes Agent** | 50 🟢 | 50 🟢 | None | 🟢 Healthy |
| **PicoClaw** | 4 🟡 | 5 🟡 | None | 🟡 Cautious |
| **NanoClaw** | 3 🟢 | 33 🟢 | None | 🟢 Healthy |
| **NullClaw** | 0 🟢 | 13 🟢 | None | 🟢 Healthy |
| **IronClaw** | 34 🟢 | 50 🟢 | None | 🟡 Cautious |
| **LobsterAI** | 0 🟢 | 21 🟢 | None | 🟢 Healthy |
| **TinyClaw** | 0 | 0 | None | 🟢 Inactive |
| **Moltis** | 0 🟢 | 1 🟡 | None | 🟢 Healthy |
| **CoPaw** | 50 🟢 | 50 🟢 | v2.0.0.post1 | 🟡 Cautious |
| **ZeptoClaw** | 0 | 0 | None | 🟢 Inactive |
| **ZeroClaw** | 50 🟢 | 50 🟢 | None | 🟡 Cautious |

- **Green (🟢)**: High activity / rapid fix cadence / stable core.
- **Yellow (🟡)**: High activity but significant regressions or review bottlenecks present.
- **Red (🔴)**: Would indicate stalled or abandoned — none present today.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale & Mindshare**: OpenClaw is the undeniable leader in raw engagement (500+ issues/PRs daily, 112 comments on a single issue). No other project approaches this community gravity.
- **Provider Ecosystem**: The fastest provider integration rate — adding Featherless, Claude Sonnet 5, Mythos 5, Meta Muse Spark 1.1, and ClawRouter in a single release. This breadth is unmatched.
- **Ecosystem Depth**: OpenClaw’s "Codex" runtime is a unique differentiation — a full developer workflow integration (CLI, GitHub) that competitors (NanoBot, Hermes) lack.

**Technical Approach Differences:**
- **Monolith-to-Module Refactoring**: OpenClaw is actively splitting 4,000+ line runtime monoliths (#106503, #106555) — a pain point already solved by NanoClaw’s modular plugin architecture.
- **Self-Healing vs. Prevention**: OpenClaw’s session init fix (#101920) adds self-healing logic; IronClaw and CoPaw are taking a more preventive, architecture-driven approach (NEA-25 unified model, v2.0.0 refactor).

**Community Size Comparison:**
- OpenClaw’s highest-engagement issue (#75) has **112 comments / 81 👍** — more than the *total* issue engagement of NanoBot, Hermes, and PicoClaw combined.
- However, OpenClaw’s **4 P0 regressions in stable** (tool placeholder string, session init conflict, database corruption) expose that scale comes with a reliability tax that focused projects like NullClaw (0 open issues) do not pay.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging across multiple projects simultaneously, indicating true ecosystem-level needs:

| Requirement | Affected Projects | Specific Pain Points |
|---|---|---|
| **Tool-Call / Message Pairing Integrity** | **CoPaw**, **OpenClaw**, **Hermes Agent** | Tool results returning placeholder strings (OpenClaw #104721), orphan `ToolResultBlock` causing 400 errors (CoPaw #5996), `(see attached image)` replacements across 3 code paths |
| **Session State Reliability** | **OpenClaw**, **Hermes Agent**, **IronClaw** | "Reply session initialization conflicted" (OpenClaw #102020), session list omissions (Hermes #38989), out-of-order messages (IronClaw #6047) |
| **Per-Provider API Key / Model Management** | **Hermes Agent**, **NanoClaw**, **OpenClaw** | Dedicated provider settings panel (Hermes #39020), default provider config (NanoClaw #2906), per-provider `errorSubstitutions` |
| **Cross-Platform Desktop Support** | **OpenClaw**, **Hermes Agent**, **LobsterAI** | Linux/Windows apps (OpenClaw #75, 112 comments), Windows installer hangs (LobsterAI #2327), IME support (Hermes #39213) |
| **Security Hardening** | **NanoClaw**, **OpenClaw**, **IronClaw**, **PicoClaw** | MCP approval smuggling (NanoClaw #2827), fs.listDir authorization (OpenClaw #105936), no private vulnerability reporting (IronClaw #6000), libolm→vodozemac migration (PicoClaw #3088) |
| **MCP Tool Access Control** | **NanoClaw**, **CoPaw**, **ZeroClaw** | Allowlist env var (NanoClaw #3037), tool denylist broken (CoPaw #5947), deferred MCP access policy (ZeroClaw #8496) |
| **Local-First / Small Model Viability** | **ZeroClaw**, **Hermes Agent**, **NanoBot** | Strict parsing, no prompt leakage (ZeroClaw #5287), weak local models reproducing steering markers (Hermes #63940), configurable verbosity (NanoBot #1500) |
| **Localization & CJK Support** | **NanoBot**, **Hermes Agent**, **ZeroClaw** | pt-BR locale (NanoBot #4914), Chinese IME support (Hermes #39213), English-only channel replies despite `zh-CN` config (ZeroClaw #6548) |

---

## 5. Differentiation Analysis

| Project | Target User | Core Differentiator | Key Weakness |
|---|---|---|---|
| **OpenClaw** | Power user / Developer | Broadest provider ecosystem, Codex runtime integration | Scale-induced instability; P0 regressions in stable |
| **NanoBot** | Individual assistant user | Strong localization support, rapid bug fix cadence | Smaller provider ecosystem, less developer tooling |
| **Hermes Agent** | Multi-channel user (Desktop/Terminal) | Best desktop UX, Chinese localization, CJK IME support | Open PR backlog (39 open), gateway reliability gaps |
| **PicoClaw** | Niche/Edge user | Lightweight, focused on caching optimization (Anthropic) | Community stagnant; stale PRs without maintainer response |
| **NanoClaw** | Plugin/Extension developer | Best modular architecture, MCP security focus, Dial channel | No releases cut; high review bandwidth needed |
| **NullClaw** | Reliability-focused user | Zero open issues; memory safety focus (use-after-free fixes) | Low feature velocity; PRs stall for weeks |
| **IronClaw** | Enterprise / High-throughput shop | Most mature extension model (NEA-25), Matrix channel skeleton | 28 open bug bash issues; security governance missing |
| **LobsterAI** | Windows/Mac enterprise user | Best installer robustness, cowork follow-up queuing | No community engagement (0 comments across all items) |
| **CoPac** (CoPaw) | Chinese-speaking power user | Strong Chinese-language community; rapid fix turnaround | v2.0.0 regressions eroding trust; 27 open issues |
| **ZeroClaw** | Orchestration / SOP user | Best deterministic pipeline features (SOP control plane) | 48 open PRs; review bottleneck; CI instability |
| **Moltis** | CalDAV user | Niche CalDAV integration focus | Inactive; single open PR for 3 days |

---

## 6. Community Momentum & Maturity

**Tier 1 — Mega-Project (Rapidly Iterating, High Risk/High Reward):**
- **OpenClaw**, **IronClaw**, **ZeroClaw**, **CoPaw**
- These projects are shipping massive architectural changes (refactoring monoliths, unified extension models, SOP pipelines) while simultaneously fighting regressions. They attract the most contributors and the most complaints.

**Tier 2 — Focused Maintainers (Healthy, Steady Cadence):**
- **NanoBot**, **NanoClaw**, **Hermes Agent**, **LobsterAI**
- These projects show high PR merge rates, low open issue counts, and responsive maintainers. They are stabilizing around specific value propositions (localization, plugins, desktop UX, installer reliability).

**Tier 3 — Niche or Stalled (Low Activity, Targeted Features):**
- **NullClaw**, **PicoClaw**, **Moltis**, **TinyClaw**, **ZeptoClaw**
- These projects have small to zero community engagement. NullClaw is functionally stable but has a PR review bottleneck. PicoClaw is losing contributor momentum. TinyClaw and ZeptoClaw are effectively idle.

**Health Observation:** The ecosystem's "tier 1" is burning hot but fragile — OpenClaw and CoPaw are both shipping regressions that actively break the core user workflow (tool output). The "tier 2" projects represent a safer, more stable choice for production deployment today.

---

## 7. Trend Signals

**Five industry trends extracted from today's community data:**

1. **“Reliability Over Features” Backlash**
   - Users are explicitly stating they would trade new providers for stability. CoPaw issue #6013 (“v2.0.0 is less stable than v1.x”) and OpenClaw’s multiple P0 regressions signal that the entire ecosystem is hitting a **quality ceiling**. Tool-call integrity is the #1 technical concern across 4 major projects.

2. **The Unresolvable Cross-Platform Gap**
   - OpenClaw’s #75 (112 comments) reveals that desktop app demand for Windows/Linux is the most-pained request in the ecosystem. Meanwhile, Hermes and LobsterAI are investing heavily in specific platforms (macOS, Windows CJK). The market seems to be fragmenting rather than converging on a universal desktop stack.

3. **Security is a Second-Class Citizen**
   - IronClaw has no `SECURITY.md` for responsible disclosure (#6000). PicoClaw’s `vodozemac` migration has been stalled for 37 days. NanoClaw had approval card smuggling that hid malicious args. The ecosystem is **reactive** on security — fixing bugs after they’re reported rather than shipping hardened defaults. This is a risk for enterprise adoption.

4. **Local-First is a Growing Requirement**
   - Multiple projects (ZeroClaw #5287, Hermes #63940, NanoBot #1500) are getting user requests for strict local model support — compact prompting, no prompt leakage, offline viability. The appetite for cloud-only AI assistants appears to be waning as token costs and privacy concerns grow.

5. **Deterministic Pipelines are the New Frontier**
   - ZeroClaw’s SOP milestone (12+ PRs for approval-gated, daemon-owned workflows) and NanoClaw’s MCP tool allowlist represent a shift from **conversational agents** to **programmatic agents**. The next competitive advantage will be reliability and auditability, not conversational polish.

**Value for AI Agent Developers:** Today’s data strongly suggests that shipping tool-call integrity and session state reliability before adding new providers is the winning strategy. The projects that fix these fundamentals (NullClaw’s use-after-free, NanoClaw’s MCP security) are earning trust, while those that prioritize feature velocity over stability are seeing user backlash.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Based on the provided GitHub data for the NanoBot project on 2026-07-13, here is the project digest for **2026-07-14**.

---

# NanoBot Project Digest — 2026-07-14

## 1. Today's Overview
The NanoBot project shows a **high level of activity** driven primarily by a significant wave of automated maintenance. In the last 24 hours, 45 pull requests (PRs) were updated, with 18 merged or closed, alongside 13 updated issues (11 closed). The volume of closed issues (11 out of 13) and merged PRs (18) indicates a strong push to resolve tickets and integrate fixes, likely part of a steady cadence of updates. However, with **27 open PRs** remaining and several carrying `conflict` labels, the project is dealing with a substantial merge queue and feature integration challenges.

## 2. Releases
**No new releases were created in the last 24 hours.**

## 3. Project Progress
The closing of **18 PRs** signals significant progress in both bug fixing and feature work. Key merges and closures include:
- **Observability & Audit:** PR [#4320](https://github.com/HKUDS/nanobot/pull/4320) (`feat(audit)`) was merged, adding a configurable audit module for agent action observability.
- **Localization:** PR [#4914](https://github.com/HKUDS/nanobot/pull/4914) was closed, adding a Brazilian Portuguese (pt-BR) locale to the WebUI.
- **Documentation:** PR [#4913](https://github.com/HKUDS/nanobot/pull/4913) and [#4912](https://github.com/HKUDS/nanobot/pull/4912) were merged, updating the changelog and fixing a broken Star History embed in the README.
- **Memory System:** PR [#4909](https://github.com/HKUDS/nanobot/pull/4909) (`fix(dream)`) was closed, fixing a bug where Dream memory diffs were incorrectly reporting line-ending-only changes as modifications.
- **Bug Fixes:** Several closed issues (#4897, #4887, #4882, #4893, #4894) indicate that fixes for Discord integration, test dependencies, Dream session pruning, and empty file diff reporting are now in the main branch.

## 4. Community Hot Topics
The most engaged discussions centered around platform integration and core functionality:
- **Mattermost Support (Issue #1011):** This [stale issue](https://github.com/HKUDS/nanobot/issues/1011) requesting Mattermost integration received 4 👍 reactions, indicating latent demand for a team-communication channel alternative to Discord and Telegram.
- **WeChat Function (Issue #192):** Another [stale request](https://github.com/HKUDS/nanobot/issues/192) for WeChat integration continues to draw positive reactions, underlining the need for broader platform support.
- **Information Flow Control (Issue #1500):** A [feature request](https://github.com/HKUDS/nanobot/issues/1500) with 1 👍 on implementing a message severity hierarchy (analogous to log levels). The author expresses frustration with the LLM dumping verbose execution details, requesting the ability to suppress unnecessary output.
- **Open Issue #4864 (Bug):** The [bug report](https://github.com/HKUDS/nanobot/issues/4864) regarding an endless loop caused by the `complete_goal` function's parameter parsing has 3 comments, suggesting active debugging.

## 5. Bugs & Stability
Several notable bugs were addressed in the last 24 hours, with corresponding fix PRs in the pipeline.

* **High Severity:**
    - **Discord Bot Integration (Issue #4897 - Closed):** A critical bug where a Discord bot would go online but fail to receive messages. The ability to close this issue suggests a fix was identified.
    - **Endless Loop in Tool Execution (Issue #4864 - Open):** An active bug where the `complete_goal` tool enters an endless loop due to a recent change in JSON serialization for tool parameters. A fix is likely a priority.
* **Medium Severity:**
    - **Heartbeat Evaluation Regression (PR #4915 - Open):** A [new PR](https://github.com/HKUDS/nanobot/pull/4915) explicitly aims to fix regressions caused by migrating the heartbeat system to a cron-based scheduler, making response evaluation more configurable.
    - **Dream Content Diffs (Issues #4882 & #4894 - Closed):** Two bugs were fixed: one where empty files were incorrectly reported as modified, and another where base64-encoded Dream session files were not being pruned.
* **Low Severity:**
    - **Test Setup (Issue #4887 - Closed):** A developer experience bug where Feishu tests failed due to a missing dependency in the default `dev` extras group was resolved.

## 6. Feature Requests & Roadmap Signals
Strong signals from the PR queue indicate the next minor release will focus on **stability, configuration, and core agent extensibility.**
- **Agent Tool Gateway (Issue #4911 - Open):** A [new enhancement request](https://github.com/HKUDS/nanobot/issues/4911) proposes a "guarded tool gateway seam" allowing channels (like a voice channel) to run the agent's tools. This is a significant architectural proposal for real-time interactions.
- **Model Presets (PR #4866 - Open):** This [feature PR](https://github.com/HKUDS/nanobot/pull/4866) to bind model presets to sessions is a strong candidate for the next version, suggesting a focus on per-session LLM configuration.
- **Workspace Write Serialization (PR #4888 - Open):** This [fix PR](https://github.com/HKUDS/nanobot/pull/4888) for serializing workspace writes is critical for preventing data races in concurrent sessions and is likely a high-priority merge.

## 7. User Feedback Summary
Real user pain points are visible across the issues:
- **Platform Lock-in:** Users (Issues #192, #1011) are actively seeking alternatives to Discord, Telegram, and Slack, naming specific privacy and usability concerns.
- **Information Overload:** Users (Issue #1500) want more granular control over the output verbosity of the agent, finding the default flow of every tool call and thinking step to be intrusive.
- **Integration Friction:** The recurring issues with Discord (Issue #4897) and Feishu (Issue #2352) highlight that even with proper API keys, the setup and runtime experience can be unreliable.
- **Windows Support:** The existence of PR [#4917](https://github.com/HKUDS/nanobot/pull/4917) to fix UTF-16 decoding on Windows suggests the Windows user base is growing and encountering platform-specific bugs.

## 8. Backlog Watch
Several open PRs with the `conflict` label require maintainer attention to resolve merge conflicts and progress towards integration.
- **PR #1599 (feat/telegram streaming):** This 4-month-old [PR](https://github.com/HKUDS/nanobot/pull/1599) for real-time LLM response streaming on Telegram is a popular feature that remains stalled due to conflicts.
- **PR #4313 (WebUI/config parity):** This extensive [PR](https://github.com/HKUDS/nanobot/pull/4313) aims to close the gap between WebUI settings and `config.json` but is also marked as conflicting.
- **PR #4587 (WebUI Markdown export):** A [feature request](https://github.com/HKUDS/nanobot/pull/4587) to export WebUI sessions as Markdown, labeled as `conflict`, suggesting it needs a rebase.
- **Stale Issues:** Issues #192 (WeChat) and #1011 (Mattermost) have been stale for 5 months. A maintainer decision (accepting, rejecting, or marking as "help wanted") would be beneficial for the community.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-14

## 1. Today's Overview

Project activity is **moderately high**, with 50 issues and 50 pull requests updated in the last 24 hours. A significant cleanup wave is underway: 29 of the 50 updated issues were closed, and 11 PRs were merged or closed. The open/active issue count (21) and open PR count (39) indicate a modestly growing backlog despite the high closure rate. No new releases were published today; the project remains focused on bug fixing and hardening after the v0.15.x cycle. Notable clusters of fixes target subprocess timeout gaps across multiple components and session state/corruption bugs in the desktop and gateway.

## 2. Releases

**No new releases today.** The latest tagged release remains v0.15.1 (2026-05-29) and the PyPI release v0.15.2 (noted in Issue #38949 as missing documented features).

## 3. Project Progress

**11 PRs were merged or closed today.** Key fixes that landed:

- **Desktop Chinese IME support (PR #39213, merged):** Comprehensive Chinese localization (zh-CN) with ~300+ translation keys, auto-detected from browser/system settings.
- **Desktop Windows composer message truncation (PR #39210, merged):** Fixed React reconciliation timing issue causing random-length message clipping on Windows.
- **OpenRouter media providers (PR #39235, closed):** Added TTS, STT, video and audio generation support under OpenRouter as a first-class media backend.
- **Hindsight mental models (PR #31869, still open):** Continues progress toward integrating mental model management into the memory plugin.

Other closed issues (not direct PRs) reflect fixes that were implemented on `main`: sidebar session list omissions, CJK IME send button visibility, gateway remote mode flapping, stale session bubbles, and various Docker/CLI/Gateway bugs.

## 4. Community Hot Topics

These issues drew the most discussion and reactions:

1. **Hermes Desktop remote gateway mode flaps back to local backend** (Issue #38873, 8 comments, 2 👍) — [Link](https://github.com/NousResearch/hermes-agent/issues/38873)  
   *User reports that after successfully validating a remote VPS backend over Tailscale, the app reverts to local backend. This is a core remote-workflow reliability concern.*

2. **Sidebar session list intermittently omits sessions** (Issue #38989, 6 comments, 3 👍) — [Link](https://github.com/NousResearch/hermes-agent/issues/38989)  
   *Sessions "disappear" from the sidebar despite being available in history — a high-frustration UX issue for users managing multiple conversations.*

3. **Auxiliary compression routes provider-qualified Gemini model to Codex backend** (Issue #39047, 5 comments) — [Link](https://github.com/NousResearch/hermes-agent/issues/39047)  
   *Configuration confusion: an `auto`-provider auxiliary task routes a Google model slug (`google/gemini-3-flash-preview`) to the Codex backend, which rejects it with HTTP 400.*

4. **Chinese IME: Enter does not submit draft text** (Issue #39025, 5 comments) and **Send button hidden during CJK IME composition** (Issue #39231, 3 comments) — These two issues reflect the same fundamental desktop composer synchronization problem with East Asian input methods, a recurring theme today.

5. **Telegram DM topic mode: root-lobby gate swallows kanban wake events** (Issue #63911, 3 comments) — [Link](https://github.com/NousResearch/hermes-agent/issues/63911)  
   *Newly opened today: a subtle session-state/message-delivery bug where Telegram topic-mode root lobbies silently ignore agent wake events when `thread_id` is empty.*

**Underlying need:** Users are pushing for full IME/CJK support in the desktop app (now addressed by the merged Chinese localization PR), more reliable remote-backend persistence, and clearer fallback/configuration behavior when multiple providers or models are in play.

## 5. Bugs & Stability

**New bugs reported today (highest severity first):**

| Issue | Severity | Status | Description | Fix PR Exists? |
|-------|----------|--------|-------------|----------------|
| #63892 — Gateway OOM via MCP poll loop | **P0** | Open | `concurrent.futures.TimeoutError` alias mismatch causes infinite traceback leak at ~108MB/s | No |
| #63860 — Stale housekeeping fallback survives substantive tool-only turn | **P1** | Open | A cached `_last_content_with_tools` response from a housekeeping-only turn can be incorrectly finalized | No |
| #26813 — Gateway: /stop and /interrupt fed as steer text instead of interrupting | **P1** | Closed | Slash commands ignored when gateway is in `steer` or `queue` mode — fixed on main | Yes (closed) |
| #63940 — Weak local models reproduce STEER_CHANNEL_NOTE marker template verbatim | **P2** | Open | Sub-8B models in Discord gateway output the steering marker instead of replying | No |
| #63849 — Tool-result images never evicted on OpenAI-compatible path | **P2** | Open | Accumulates screenshots until local model OOM; eviction mechanism missing | No |
| #64020 — Failing payment method on subscription setup | **P2** | Open | User cannot proceed with free plan due to card being declined | No |
| #63895 — Terminal autoscrolls to bottom after agent finishes | **P2** | Open | User cannot review history because view auto-scrolls periodically | No |

**Regression risk flagged:** Multiple open PRs carry `sweeper:risk-session-state` or `sweeper:risk-message-delivery` labels, indicating maintainer caution around session integrity changes.

**Notable fix PRs opened today:**
- PR #63979 — Add timeout to SSH `tar/ssh` pipe cleanup (P3, risk: moderate)
- PR #63915 — Guard cron `tick()` against double-close of lock_fd (fixes `ValueError: I/O operation on closed file`)
- PR #64076 — Reduce `SELECT *` in `get_compression_lineage` to 4 columns (perf optimization)

## 6. Feature Requests & Roadmap Signals

**New features requested today:**

1. **Native fallback-chain readiness check without full agent sessions** (Issue #63852) — [Link](https://github.com/NousResearch/hermes-agent/issues/63852)  
   *User wants a lightweight command to verify that configured fallback models actually work at inference time, beyond just listing them. If adopted, this would reduce configuration friction for multi-provider setups.*

2. **Per-provider API key management in Desktop settings** (Issue #39020, closed with fix on main) — [Link](https://github.com/NousResearch/hermes-agent/issues/39020)  
   *Users want a dedicated "Providers" settings panel with enable/disable toggles and per-provider API key fields. Now implemented, per issue closure.*

3. **Separate cron/autonomous sessions from manual chats in Desktop** (Issue #38894, closed with fix on main) — [Link](https://github.com/NousResearch/hermes-agent/issues/38894)  
   *Scheduled/autonomous sessions were flooding the manual-chat session list. Now implemented.*

**Prediction for next release:** The provider management UI, CJK IME support, session filtering by type, and the fallback-chain readiness check are strong candidates for the v0.15.3 or v0.16.0 release based on the volume of related closed issues today.

## 7. User Feedback Summary

**Pain points expressed today:**

- **Desktop reliability:** Multiple users report session list omission, stale UI state when switching sessions, and composer artifacts during CJK IME use. These are now largely fixed on `main`.
- **Windows CLI missing `hermes` command:** User (AnasBroukpro) reports that only `hermes-agent.exe` and `hermes-acp.exe` are created in `venv/Scripts/`, with no `hermes.exe` on PATH (Issue #39185, closed/fixed).
- **Docker persistence frustration:** User (dima-online) notes that WhatsApp dependencies installed inside the official Docker container are destroyed on next image pull — calls for a persistent volume or pre-baked plugin approach (Issue #39220, closed/fixed).
- **Payment/subscription friction:** New user (curiouscurrent) reports inability to proceed despite selecting the free plan — card declined, no workaround provided (Issue #64020, still open).
- **Multi-provider confusion:** Users continue to encounter unexpected routing of auxiliary tasks to wrong providers (e.g., Google model → Codex backend, Issue #39047).

**Satisfaction signals:** The Chinese localization PR (#39213) received positive engagement, and the rapid closure of 11 PRs today suggests maintainers are responsive to high-pain issues.

## 8. Backlog Watch

**Unanswered or long-open items needing maintainer attention:**

1. **PR #55037 — Z.AI concurrency bound under subagent swarms** (P2, still open since June 29) — [Link](https://github.com/NousResearch/hermes-agent/pull/55037)  
   *Adds strict concurrency control for Zhipu AI calls to prevent HTTP 429 overload. No maintainer activity in last 24h; 15 days open.*

2. **PR #31869 — Hindsight mental models support** (P3, open since May 25) — [Link](https://github.com/NousResearch/hermes-agent/pull/31869)  
   *Large feature addition (6 new tools). Updated today but no maintainer comment on timeline or merge blockers. 51 days open.*

3. **PR #39226 — Fix browser_vision embed-time pixel/byte caps** (P2, open since June 4) — [Link](https://github.com/NousResearch/hermes-agent/pull/39226)  
   *Prevents `browser_vision` from passing raw full-resolution screenshots when inline caps should apply. 41 days open.*

4. **PR #39209 — Include tool_choice parameter in vLLM requests** (P2, open since June 4) — [Link](https://github.com/NousResearch/hermes-agent/pull/39209)  
   *Without this fix, vLLM backends never invoke tools. Critical for any vLLM user. 41 days open.*

5. **Issue #64020 — Failing payment method** (P2, open since yesterday) — [Link](https://github.com/NousResearch/hermes-agent/issues/64020)  
   *New user blocked from on-boarding. Needs a response or workaround to unblock the user.*

6. **Issue #63892 — Gateway OOM via MCP poll loop** (P0, open since yesterday) — [Link](https://github.com/NousResearch/hermes-agent/issues/63892)  
   *Memory leak at 108MB/s. The highest-severity open issue. No PR or maintainer response yet.*

**Overall assessment:** The project is in a healthy but high-velocity state — bugs are being closed rapidly, but the open PR backlog (39 open PRs) and several long-stalled feature PRs suggest that maintainer capacity may be becoming a bottleneck. The P0 memory leak in the MCP poll loop (#63892) warrants immediate attention.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-14

## Today's Overview
PicoClaw shows a steady maintenance cadence with 4 open issues and 5 pull requests updated in the last 24 hours, all from the open-source community. Notably, all 4 tracked issues remain open with no new resolutions, while the single merged PR (#3253) introduces webhook functionality for the gateway layer. No new releases were published today, but the activity signals ongoing community engagement around caching, provider compatibility, and security hardening. The project's pulse remains moderate but healthy, with several "stale" items lingering without maintainer response.

## Releases
**No new releases** have been published in the reported period. The latest available version remains within the 0.2.9–0.3.1 range (referenced in Issue #3230).

## Project Progress
- **PR #3253** — [MERGED] Feat/gateway webhook (author: tisoga, merged 2026-07-13). This closed PR adds webhook support for the gateway, likely enabling external event-driven integrations. No details on breaking changes or migration notes were included in the summary.
- **PR #3228** — Still open; proposes Anthropic prompt caching via `cache_control` on system blocks.
- **PR #3192** — Still open; Docker base image bump (alpine 3.21 → 3.23).
- **PR #3191** — Still open; duplicate `.gitignore` cleanup.
- **PR #3254** — Newly opened today; fixes model resolution priority in agent configuration.

No feature branches were fully merged except the webhook PR.

## Community Hot Topics
1. **Issue #3088** — *Use vodozemac instead of libolm* (👍2, 8 comments)  
   [Sipeed/PicoClaw Issue #3088](https://github.com/sipeed/picoclaw/issues/3088)  
   The most active discussion, advocating for replacing the unmaintained `libolm` with `vodozemac` (the official Matrix replacement). The community wants compile-time optionality and improved security. This has been open since June 9, tagged `help wanted` and `priority: high`, but remains stale.

2. **Issue #3231** — *SearXNG base auth header requirement* (👍0, 1 comment)  
   [Sipeed/PicoClaw Issue #3231](https://github.com/sipeed/picoclaw/issues/3231)  
   A Chinese-language request to support HTTP Basic Auth headers for SearXNG search integration, noting that appending credentials to the URL doesn't work. Indicates specific search provider pain.

3. **Issue #3229** — *Rolling conversation cache breakpoints for Anthropic* (👍0, 1 comment)  
   [Sipeed/PicoClaw Issue #3229](https://github.com/sipeed/picoclaw/issues/3229)  
   Proposes extending the fix in PR #3228 with per-block `cache_control` for conversation history (not just system prompts). Shows advanced caching demands in agentic workloads.

## Bugs & Stability
| Bug | Severity | Fix PR Existing? |
|-----|----------|------------------|
| **Issue #3230** — *Gemini API missing thought_signature via OpenAI compat format* | **High** — blocks tool-use calls with Gemini through Cloudflare AI Gateway | No |  
| **Issue #3231** — *SearXNG auth fails without basicauth header* | Medium — breaks third-party search integration | No |

The Gemini `thought_signature` error is the most impactful reported bug today, affecting all versions 0.2.9 to 0.3.1 when calling Gemini via OpenAI-compatible format through Cloudflare AI Gateway. No incoming fix PR has been associated.

## Feature Requests & Roadmap Signals
- **vodozemac replacement (Issue #3088)** — The highest-priority `help wanted` issue. Likely for next minor release if maintainers respond.
- **Anthropic prompt caching on conversation history (Issue #3229)** — Complements PR #3228; could land together in a caching-focused release.
- **SearXNG Basic Auth support (Issue #3231)** — Niche but blocking for Chinese/enterprise users.
- **Gemini OpenAI-compat fix (Issue #3230)** — Bug, not a feature, but fixing it would unblock multi-provider setups.

**Prediction for next version (0.3.2 or 0.4.0):** At least one Anthropic caching improvement and the webhook gateway feature (already merged) are likely to ship next. The vodozemac migration may be deferred due to its scope.

## User Feedback Summary
- **Pain Points:** Users report that Anthropic prompt caching is unusable on the `anthropic-messages` provider (#3088/#3229). The Gemini API compatibility layer is broken for tool calls (#3230). SearXNG integration lacks proper authentication (#3231). One user notes that the `libolm` dependency is a security risk (#3088).
- **Use Cases:** Clear demand for production-ready caching in agentic loop workflows (Anthropic heavy users). Multi-provider setups (Gemini + OpenAI format) failing in real deployments.
- **Satisfaction:** No overtly positive feedback captured today. The high number of stale but unaddressed issues suggests some frustration among active contributors.

## Backlog Watch
- **Issue #3088** — *vodozemac migration* (created 2026-06-09, stale) — High priority, 8 comments, no maintainer response. Community solution proposed but unaddressed.
- **Issue #3230** — *Gemini missing thought_signature* (created 2026-07-06, stale) — Critical bug, no maintainer acknowledgment.
- **PR #3192** — *Docker image bump* (created 2026-06-27, stale) — Simple chore but not merged for 17 days.
- **PR #3191** — *.gitignore cleanup* (created 2026-06-27, stale) — Identical stall pattern.

These items risk contributor burnout if left unaddressed much longer. The vodozemac issue in particular has strong community consensus and a clear implementation path.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-14

## 1. Today's Overview

The NanoClaw project shows **very high activity** over the past 24 hours, with 33 pull requests updated (27 merged/closed, 6 open) and 3 issues resolved. All three updated issues were closed, indicating strong maintenance velocity. The project's core team and external contributors are pushing multiple concurrent feature streams: persistent memory systems, new channel integrations (Dial), structured skill formats, and MCP security hardening. No new releases were published today, but the volume of merged PRs (27) suggests a significant release may be imminent.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

**27 pull requests were merged or closed** in the last day, spanning several major work streams:

**New Channels & Integrations**
- **Dial channel adapter** (PR #3032, merged) — Adds native SMS/MMS and AI voice call support via `@getdial/sdk`, with long-text chunking and error handling
- **Dial setup integration** (PR #3033, merged) — First-class option in `pnpm run setup:auto` picker, with `/add-dial` install skill

**Structured Skill Format**
- **Channel install via SKILL.md** (PR #3035, merged, core-team) — Setup wizard now applies the SKILL.md document directly to install channels, eliminating bespoke per-channel wizard flows

**Scheduled Tasks & Templates**
- **Scheduled tasks in templates** (PR #3022, merged, core-team) — Templates can define recurring cron tasks; created paused when agent group is stamped

**Memory System**
- **Provider-agnostic persistent memory** (PR #3012, open) — Shared memory tree across agent providers, loaded on new contexts (startup/clear/compact)
- **Codex memory loading** (PR #3013, open) — Counterpart that loads shared memory on session start

**Core Fixes**
- **Missing channel adapter handling** (PR #2226, merged) — Throw `MissingChannelAdapterError` so retry loop runs instead of silently dropping messages
- **Missing-adapter retry routing** (PR #2996, merged, core-team) — Routes missing-adapter messages into the retry path
- **Full MCP payload on approval card** (PR #2998, merged, core-team) — Fixes security gap where `args` and `env` were hidden from approvers
- **Wiring ACL creation** (PR #2938, merged, core-team) — `ncl wirings create` now auto-creates `agent_destinations` ACL row
- **Default agent provider** (PR #2906, merged, core-team) — Instance-wide default via `DEFAULT_AGENT_PROVIDER` in `.env`
- **Provider output substitutions** (PR #2120, merged) — Per-provider `errorSubstitutions` for cleaner error messages
- **Soft error logging** (PR #2966, merged, core-team) — Log when errored batch is acked completed

**Infrastructure**
- **Silent-wiring fix** (PR #2743, merged) — `ncl wirings create` now creates the required `agent_destinations` side effect
- **Scheduled-task time injection** (PR #3036, open) — Injects `current_time` into context header with weekday

---

## 4. Community Hot Topics

All 33 PRs and 3 issues today have **zero comments and zero reactions**, which is unusual and may indicate these are either automated or tracked externally. The most active PRs by substance:

**#3037** (open, 2026-07-13) — *MCP tool allowlist*  
- Adds `NANOCLAW_MCP_TOOL_ALLOWLIST` env var to restrict available MCP tools  
- Addresses security/operational control need: operators want granular tool access control  
- [GitHub](https://github.com/nanocoai/nanoclaw/pull/3037)

**#3036** (open, 2026-07-13) — *Time injection for scheduled tasks*  
- Injects current time with weekday into context header; fixes agent confusion on cron turns  
- Responds to a real user pain point (agent misidentifying day-of-week)  
- [GitHub](https://github.com/nanocoai/nanoclaw/pull/3036)

**#3012 / #3013** (both open, core-team) — *Persistent memory + Codex loading*  
- Two-part provider-agnostic memory system  
- High architectural significance; likely to land in next release together  
- [GitHub (#3012)](https://github.com/nanocoai/nanoclaw/pull/3012) | [GitHub (#3013)](https://github.com/nanocoai/nanoclaw/pull/3013)

**Underlying need analysis:** The community (especially core team) is pushing for **multi-provider support** (default provider, memory abstraction) and **operational safety** (MCP allowlists, approval card transparency, missing-adapter handling).

---

## 5. Bugs & Stability

**High Severity**  
- **MCP approval smuggling vulnerabilities** (Issues #2827, #2762 — both closed with PR #2998)  
  - Approval card showed only server name and base URL; `args` and `env` were hidden  
  - Attacker could embed malicious CLI args or environment variables  
  - **Fixed in PR #2998** (merged) — renders full payload on the approval card  
  - [Issue #2827](https://github.com/nanocoai/nanoclaw/issues/2827) | [Issue #2762](https://github.com/nanocoai/nanoclaw/issues/2762) | [PR #2998](https://github.com/nanocoai/nanoclaw/pull/2998)

**Medium Severity**  
- **Outbound messages to offline channel adapter marked delivered** (Issue #2995 — closed)  
  - When channel adapter is unregistered, delivery loop marks message as delivered without sending  
  - States: missing credentials, factory returned null, setup failed, offline instance  
  - **Fixed via PR #2996** (merged) — routes into retry path; **PR #2226** (merged) — throws error  
  - [Issue #2995](https://github.com/nanocoai/nanoclaw/issues/2995) | [PR #2996](https://github.com/nanocoai/nanoclaw/pull/2996) | [PR #2226](https://github.com/nanocoai/nanoclaw/pull/2226)

**Medium Severity**  
- **Silent data loss in cleanup script** (PR #1889 — merged)  
  - `cleanup-sessions` script treated sqlite3 failures as "no active sessions", silently deleting data  
  - **Fixed** — hard-fail when sqlite3 is missing or query errors  
  - [PR #1889](https://github.com/nanocoai/nanoclaw/pull/1889)

**Low Severity**  
- **Diagnostics opt-out gap** (PR #1887 — merged)  
  - `ph_event` didn't honor `DO_NOT_TRACK` env var; only project-specific `NANOCLAW_NO_DIAGNOSTICS`  
  - **Fixed** — also checks `DO_NOT_TRACK` and skips if curl is missing  
  - [PR #1887](https://github.com/nanocoai/nanoclaw/pull/1887)

---

## 6. Feature Requests & Roadmap Signals

**Likely to land in next version:**

1. **MCP Tool Allowlist** (PR #3037, open) — `NANOCLAW_MCP_TOOL_ALLOWLIST` env var for restricting available tools by name. Signals operator demand for fine-grained MCP access control in production.

2. **Persistent Memory System** (PRs #3012, #3013, open) — Provider-agnostic memory tree shared across agent providers with Codex integration. This is a major architectural addition that enables cross-session state.

3. **Time Context Enhancement** (PR #3036, open) — Injects current time + weekday into context header. Addresses a clear usability bug (agent confusion on day-of-week).

4. **Socket Security Hardening** (PR #2802, open) — Client timeout/cap and server fail-closed behavior for `ncl socket` transport. Production security requirement.

**Predictions:** The memory system (#3012/#3013) and MCP allowlist (#3037) are clear next-release candidates given core-team authorship and high architectural significance. The Dial channel (#3032/#3033) is already merged and will ship in the next release.

---

## 7. User Feedback Summary

**Pain Points (addressed or visible in fixes):**
- **Security concern:** Approval flow could hide malicious args/env from approvers (issues #2827, #2762) — now fixed
- **Message delivery failures:** Silent drops when channel adapter is offline (issue #2995) — now fixed
- **Agent day-of-week confusion:** Scheduled tasks misidentifying weekdays (PR #3036) — fix in progress
- **Missing ACL side effects:** `ncl wirings create` silently dropped agent destinations (PR #2743) — now fixed
- **Diagnostics privacy:** `DO_NOT_TRACK` env var not respected (PR #1887) — now fixed

**User satisfaction signals:** The rapid closure of 3 issues (all security/functionality bugs) and 27 merged PRs in 24 hours suggests a responsive maintainer team. No negative sentiment is visible in the data, but the absence of comments/reactions on any issue or PR makes it hard to gauge community engagement directly.

---

## 8. Backlog Watch

**Critical open PR needing attention:**

- **Socket security hardening** (PR #2802, open since 2026-06-17, ~27 days)  
  Addresses unbounded response buffer and no-request-timeout issues in `ncl socket` transport. This is a **security vulnerability** — a malicious host can leave promises unsettled forever or grow memory without limit. Despite being open for nearly a month, it has no comments or reactions.  
  [GitHub](https://github.com/nanocoai/nanoclaw/pull/2802)

**Other open PRs worth monitoring:**

- **MCP tool allowlist** (PR #3037, open since 2026-07-13, ~1 day) — New, no risk yet
- **Time context injection** (PR #3036, open since 2026-07-13, ~1 day) — New, no risk yet
- **Persistent memory** (PR #3012, open since 2026-07-10, ~4 days) — Core-team, likely tracked
- **Codex memory loading** (PR #3013, open since 2026-07-10, ~4 days) — Core-team, likely tracked

**No long-stale issues** detected — all current issues were resolved within 1-5 days of their creation date. The project maintains a healthy triage cadence.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-07-14**.

---

## NullClaw Project Digest: 2026-07-14

### 1. Today's Overview
Project activity is moderate today, characterized by a strong maintenance push. While there are **zero new issues** and **zero new releases**, the project saw **13 Pull Requests updated** in the last 24 hours, all of which remain **open**. This high PR velocity suggests a significant review and iteration backlog. The focus appears to be on hardening core infrastructure—fixing channel connectivity (Discord, Weixin), enhancing security (token persistence, JWT handling), and improving the developer/user experience (REPL editor, memory controls). The lack of merged PRs today indicates that maintainers are likely deep in code review rather than merging.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
No Pull Requests were merged or closed in the last 24 hours. However, the following open PRs represent the current vector of work advancing toward completion:

- **Agent & CLI UX:**
    - **#970**: A new allocation-free line editor for the REPL is proposed, enabling arrow keys and history navigation.
    - **#964**: Enables native API-level tool calls during streaming, a core feature for real-time agent responses.
- **Memory & Configuration:**
    - **#961**: Adds configurable `auto_recall`, `recall_limit`, and `max_context_bytes` to memory, giving users granular control over context injection.
- **Channel Resilience:**
    - **#953**: Fixes the Discord gateway by recovering closed sockets, preventing silent disconnections.
    - **#968**: Persists the Matrix sync cursor (`next_batch`) across restarts to prevent re-running full initial syncs (which cause duplicate message processing).

### 4. Community Hot Topics
*(Note: Comment/react counts are `undefined` in the data, so this analysis is based on topic interest and complexity.)*

- **PR #969: Structured approval_request / approval_response flow** — This is a significant UX and safety improvement. It introduces a two-turn approval flow for dangerous tools (like shell), emitting events via SSE so channels can render a UI prompt. This addresses a core safety requirement for autonomous agents.
- **PR #964: Enable native API-level tool calls during streaming** — A technically complex change that allows the agent to execute tool calls received during a streamed response. This is critical for integrating with modern streaming LLM APIs that intermix text and tool calls.
- **PR #970: fix(cli): handle arrow keys in agent REPL** — While a "fix," this is a high-visibility improvement for developers using the CLI, addressing a basic usability pain point.

### 5. Bugs & Stability
No new bugs were reported today. However, the following **high-severity fixes** are actively in review:

- **High Severity: Use-After-Free (Cron Jobs):** PR #954 addresses a root cause of silent message delivery failures in one-shot cron jobs. The root cause is a `use-after-free` on `OutboundMessage.channel`. This is a critical memory safety issue.
- **High Severity: Discord Gateway Disconnection:** PR #953 fixes a bug where Discord gateway sockets close without recovery, leading to a complete loss of Discord bot functionality until restart.
- **Medium Severity: Android HTTP Failures:** PR #966 patches a DNS resolution failure (`NameServerFailure`) on Android (Termux) by implementing a secure buffered curl fallback.
- **Medium Severity: Matrix Initial Sync Loop:** PR #968 fixes a bug where the Matrix channel re-downloads the entire sync state on every restart due to an unsaved cursor.

### 6. Feature Requests & Roadmap Signals
While no new issues were filed today, the open PRs strongly signal the project's roadmap direction:

- **Granular Memory Control:** PR #961 (`auto_recall`, `recall_limit`) suggests that user feedback has indicated the memory system is either too aggressive or consumes too many tokens. The next version will likely include these configuration knobs.
- **Security & Authentication Hardening:**
    - PR #959 persists the paired token for cron tool access (encrypted via SecretStore), enabling secure long-running scheduled tasks.
    - PR #958 fixes a JWT claim parsing error for Microsoft Teams, improving enterprise connectivity.
- **Platform Specifics:** PR #966 (Android) and PR #963 (Weixin iLink documentation) show ongoing effort to support niche but important deployment environments and communication protocols.

### 7. User Feedback Summary
While direct user comments are not available, the PR titles reveal clear user pain points:
- **Pain: Silent failures.** The most significant pain point is silent failures (e.g., cron jobs not delivering messages in #954, Discord disconnecting without warning in #953).
- **Pain: Repeated work.** Users on Matrix are experiencing duplicate processing after restarts due to the lack of state persistence (#968).
- **Pain: CLI usability.** Developers using the agent REPL on POSIX systems are frustrated by raw control characters being printed instead of arrow-key navigation (#970).
- **Pain: Mobile compatibility.** Users on Android/Termux face DNS resolution issues, breaking HTTP connectivity (#966).

### 8. Backlog Watch
No issues are currently open, suggesting a clean backlog. However, the **13 open PRs** represent a significant review burden. The following PRs are older than two weeks and risk becoming stale if not addressed:

- **PR #953 (fix(discord))** — Opened 2026-06-12. A critical stability fix for Discord users.
- **PR #954 (fix: one-shot cron jobs)** — Opened 2026-06-13. Addresses a use-after-free bug.
- **PR #956 (ci(deps): bump alpine)** — Opened 2026-06-15. A simple dependency bump that is likely low-risk but is sitting unreviewed.
- **PR #966 (fix(http): secure buffered curl fallback on Android)** — Opened 2026-06-19. A platform-specific fix that blocks Android users from using the project reliably.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-14

## Today's Overview

IronClaw remains in an intense development and bug-fixing phase, with **84 total updates** (34 issues, 50 PRs) in the last 24 hours. Activity is dominated by **core team members** (BenKurrek, henrypark133) advancing the **NEA-25 unified extension model** — a major architectural roll-up that consolidates Slack, extension lifecycle, and channel-surface logic. The **bug_bash_P2** and **P3** issues continue to pour in (28 open), indicating the project is under active QA/stabilization scrutiny. No new releases were cut today, suggesting the team is holding for the NEA-25 train to land before tagging the next version. The **Matrix channel skeleton PR (#6062)** was closed/merged, signaling expansion of the extension ecosystem beyond Slack.

---

## Releases

**None.** No new versions or tags were published today.

---

## Project Progress

**16 PRs merged/closed** in the last 24 hours. Notable advances:

| PR | Description | Impact |
|---|---|---|
| **#6062** (CLOSED) | `feat(matrix): add Reborn channel skeleton` | Merged by new contributor `theredspoon`. Adds the WASM Matrix channel skeleton under `channels-src/matrix/` — loadable component shape, host-managed manifest, CI gates, runtime smoke tests. Lays foundation for Matrix.org integration. |
| **#6061** (OPEN) | `feat(reborn)!: unified extension model — NEA-25 Train A roll-up (#5833-#5850)` | Massive 8-PR atomic roll-up of the entire NEA-25 taxonomy stack. Single reviewable unit delivering the complete extension model redesign. This is the **main event** — merging this unblocks downstream work. |
| **#5957** (CLOSED) | `fix(reborn): harden OAuth and per-user extension lifecycles` | Combines Slack OAuth fixes, generic extension-removal cleanup, and explicit ownership migration for production installs. |
| **#6058** (CLOSED) | `build(reborn): ship extension ownership migration` | Ships the explicit extension-ownership migration binary in the Reborn runtime image, with cargo-chef caching. |
| **#5971** (CLOSED) | `fix: carry storage error cause when compaction summary persistence fails` | Fixes discarded `SessionThreadError` in compaction persistence — no more opaque failures. |
| **#6021** (CLOSED) | `build(deps): bump everything-else group (22 updates)` | Dependency bumps including `agent-client-protocol` 0.10.4→1.2.0 and various Rust ecosystem updates. |
| **#6064** (OPEN) | `fix: clear stale chat history load banner` | Fix for Issue #6050 — clears stale error banners once current-session messages load. PR exists. |

**NEA-25 Stack** (still open/in flight):
- **#5842** (stack 3/7): Extension-surface discovery replaces connectable-channels rail
- **#5845** (stack 4/7): One Slack extension (retires slack_bot/slack_personal)
- **#5847** (stack 5/7): Wire carries runtime+surfaces, not conflated kind
- **#6056** (stack 8/9): P7a — wire state enums + accounts list + deferred legs

---

## Community Hot Topics

The most active discussions center on **QA-stability issues** and **security reporting**:

| Item | Comments | Underlying Need |
|---|---|---|
| **Issue #5948** — "Assistant incorrectly reports GitHub extension as activated when it is only installed" | 5 | **Trust & transparency**: Users need accurate status reflection. Falsely reporting activation erodes confidence. Linked to the NEA-25 unified model's status-wiring. |
| **Issue #6050** — "Conversation history error banner displayed despite successful chat response" | 2 | **UX fidelity**: Stale error banners mislead users. Fix PR **#6064** already open — good response time. |
| **Issue #5640** — "Harness gap: no RecordingSecurityAuditSink double" | 2 | **Testing completeness**: Integration harness missing production wiring parity. Affects ability to test security audit paths. |
| **Issue #5741** — "builtin.http.save fails with OutputTooLarge instead of saving large responses" | 2 | **Tooling utility**: Users hitting real-world limits (saving ESPN articles) — tool should handle large responses gracefully. |
| **Issue #6000** — "How should security issues be reported?" | 1 | **Security process gap**: No `SECURITY.md`, private vulnerability reporting disabled. This is a **governance risk** — researchers cannot responsibly disclose. |
| **PR #6061** — NEA-25 Train A roll-up | 0 (but blockbuster PR) | **Architecture convergence**: The community (and internal teams) are waiting for this to land. It supersedes 8 stacked PRs and changes the extension model fundamentally. |

---

## Bugs & Stability

**28 open issues**, 14 new since last digest. Ranked by severity:

### P1 (Critical)
- **[Bug_bash_P1] Issue #5943** — "Slack DM action posts to current channel instead of user's direct messages." **No fix PR yet.** Fundamental misrouting of channel selection logic. High user-impact — private messages leak to public channels.

### P2 (High)
- **Issue #5836** — "Routine fails on every scheduled run with 'No thread attached'." 0% success rate. **No fix PR.** Systemic issue preventing all scheduled routines from working.
- **Issue #5885** — "Approval notification opens action without showing approval message." **No fix PR.** Users cannot approve/deny actions.
- **Issue #5879** — "Stale error banner remains visible after successful follow-up response." Fix direction likely similar to #6050/#6064.
- **Issue #6048** — "Agent run fails because model attempts to call an unavailable tool." **No fix PR.** Blocks multi-step workspace tasks.
- **Issue #6047** — "Task messages processed and displayed out of chronological order." **No fix PR.** Breaks conversation flow.
- **Issue #6046** — "Simple email-to-sheet workflow invokes 124 tool invocations." **No fix PR.** Efficiency regression — tool call explosion.
- **Issue #6045** — "Agent diagnoses root cause instead of accomplishing the user's intent." **No fix PR.** Agent stops at diagnosis, doesn't auto-retry with fix.
- **Issue #6044** — "Enter key sometimes does not submit message in WebUI." **No fix PR.** Intermittent UI bug.
- **Issue #6043** — "GitHub connection flow fails with generic capability error instead of starting authentication." **No fix PR.** Blocks GitHub onboarding.
- **Issue #5882** — "Repeated Slack reconnect attempts leave auth flow in broken state." **No fix PR.** Requires extension removal to recover.
- **Issue #5707** — "Routine creation response exposes internal implementation details." **No fix PR.** Security/information disclosure issue.

### P3 (Medium)
- **Issue #6051** — "Large documents labeled with warning icon instead of informational status." Misleading UX.
- **Issue #6049** — "Gmail disconnect fails with generic validation error." No explanation provided.
- **Issue #6052** — "Extensions Registry takes up to 10 seconds to load." Performance concern.
- **Issue #6029** — "GitHub extension cannot be deactivated, reconfigured, or uninstalled after activation." Lifecycle management missing.
- **Issue #6028** — "MCP tab: stray '$' rendered before heading." Minor UI rendering bug.
- **Issue #6037** — "Chat connection status is hidden during disconnects." Users cannot tell if chat is broken.
- **Issue #6039** — "Light theme has unreadable button and status colors." Accessibility regression.

### Security
- **Issue #6000** — "No SECURITY.md, private vulnerability reporting disabled." **Governance gap — no fix PR.** External reporter cannot disclose responsibly. Needs immediate attention.

---

## Feature Requests & Roadmap Signals

| Signal | Source | Likely Timeline |
|---|---|---|
| **Matrix channel support** | Merged PR #6062 (skeleton) | **Next release** — skeleton exists, will be fleshed out |
| **Per-user MCP registration** | Open PR #5970 (T1) | **Next release** — foundational for MCP ecosystem |
| **Tools-capable completion nudge** | Open PR #6013 | **Next release** — improves coding agent UX |
| **Offline v1-to-Reborn migration** | Open PR #5936 | **Next release** — critical for enterprise adoption |
| **NEA-25 unified extension model** | Open PR #6061 (Train A roll-up) | **Imminent** — this is the top priority blockbuster PR |
| **Security.md / private reporting** | Issue #6000 | **Should be urgent** — no response from maintainers yet |

---

## User Feedback Summary

Pain points cluster into **three themes**:

**1. Extension lifecycle fragility (most noise)**
> "GitHub extension cannot be deactivated, reconfigured, or uninstalled after activation." — think-in-universe
> "Repeated Slack reconnect attempts leave auth flow in broken state." — joe-rlo
> "Gmail disconnect fails with generic validation error." — joe-rlo
> "Assistant reports GitHub as activated when only installed." — joe-rlo

**2. Agent intelligence/reliability gaps**
> "Agent diagnoses root cause instead of fixing it." — joe-rlo (multiple examples)
> "Simple email-to-sheet workflow invokes 124 tool invocations." — joe-rlo
> "Agent fails because model calls unavailable tool." — joe-rlo
> "Slack DM posts to channel instead of DMs." — joe-rlo

**3. Trust-destroying UX**
> "Stale error banners persist after success." — joe-rlo (multiple issues)
> "Messages displayed out of chronological order." — joe-rlo
> "Enter key sometimes doesn't submit." — joe-rlo
> "No connection status shown during disconnect." — italic-jinxin

**Positive signal**: Matrix channel skeleton was contributed by a **new contributor** (`theredspoon`), suggesting the project's extensibility model is attracting external developers.

---

## Backlog Watch

Items needing maintainer attention:

| Item | Age | Status | Concern |
|---|---|---|---|
| **Issue #6000** — "How should security issues be reported?" | 3 days | **No response** | Security governance gap. External researcher has findings they cannot share responsibly. **Highest priority for triage.** |
| **Issue #5640** — "Harness gap: RecordingSecurityAuditSink double" | 10 days | 2 comments, no fix PR | Testing completeness gap affects ability to validate security audit paths. |
| **Issue #5741** — "builtin.http.save fails with OutputTooLarge" | 8 days | 2 comments, no fix PR | Real-world use case blocked. Affects ability to save web pages. |
| **PR #5598** — "chore: release" (version bump) | 11 days | Open, stale | Blocked on NEA-25 landing? The `ironclaw` crate would jump from 0.24.0→0.29.1 with breaking changes in `ironclaw_common` and `ironclaw_skills`. Should be unblocked once Train A merges. |
| **Issue #5836** — "Routine fails on every scheduled run" | 6 days | **No fix PR** | 0% success rate for all scheduled routines — systemic blocker for automation users. |

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-14

## Today's Overview
LobsterAI saw an exceptionally active day with 21 PRs updated in the last 24 hours, 19 of which were closed or merged. No new releases or new issues were filed. The development velocity is very high, with a clear focus on Windows installer reliability, macOS update fixes, desktop notification upgrades, and cowork (cowork) follow-up routing enhancements. Two PRs remain open: a stale dependency bump from April and a stale bug fix from April, suggesting some backlog accumulation.

## Releases
No new releases were published today.

## Project Progress
**19 PRs were closed/merged today**, spanning build system improvements, cowork stability, and UI/UX enhancements:

### Build & Platform
- **#2327** — Fixed Windows binary signing via internal Youdao signing service, preventing security software from freezing on unsigned LobsterAI.exe during installation.
- **#2326** — Self-healing Windows installer: NSIS now tries system `tar.exe` first, falls back to bundled extractor with a 10-minute watchdog.
- **#2323** — Added opt-in Windows web installer target (NSIS Web), gated by `LOBSTERAI_WEB_INSTALLER`.
- **#2328** — Fixed Chrome leaks by serializing concurrent browser launch/search operations.
- **#2321** — Fixed macOS update `hdiutil` failure.

### Cowork & Notifications
- **#2318** — Upgraded desktop notifications: `TaskCompletionNotifier` renamed to `DesktopNotificationManager`, now shows waiting notifications for permission requests/questions, foreground notification mode, tracked resolved requests.
- **#2324** — Stream ordered thinking blocks for OpenClaw (thinking displayed per-turn before tools/response, preventing duplicate messages).
- **#2319** — Revamped homepage quick-action scenarios: "教育学习" replaced with "文档写作" (docx skill), refreshed prompts, chip bar stays visible after category selection.
- **#2325** — Fixed badge/title descender clipping and stabilized template.
- **#2315** — Connected queued follow-up coordinator to process follow-ups across sessions and while app is minimized.
- **#2292** — Stabilized steer follow-up routing with Codex-style queuing, replaced temporary sessions with real started sessions.
- **#2300** — Support attachments in steer queue: file drag/paste, selected text, image payloads with lightweight snapshots.
- **#2320** — Fast-forward missed cron jobs instead of just skipping catch-up, preventing replay of every missed recurring job.

### UI/UX & General Fixes
- **#2322** — Optimized file card display.
- **#2316** — Prevented Windows title bar logo compression when sidebar collapsed with update badge.
- **#2289** — Cleared stalled compaction retry maintenance, added regression coverage.

## Community Hot Topics
No issues or PRs had any comments or reactions today. Activity is entirely maintainer-driven, with no external community engagement visible in the last 24 hours.

## Bugs & Stability

### Critical
- **Windows installer hangs** (PRs #2327, #2326): Security software froze on unsigned `LobsterAI.exe` during installation, causing hanging installs and corrupted state. Both fix PRs were merged today.
- **Chrome leaks** (PR #2328): Concurrent browser launch/search was causing Chrome process leaks. Fix merged.

### High
- **macOS update `hdiutil` failure** (PR #2321): Update process broken on macOS. Fix merged.
- **Stalled compaction retry maintenance** (PR #2289): Context maintenance not cleared when compaction retry never resumed. Fix merged.

### Medium
- **Badge/title descender clipping** (PR #2325): Visual defect in cowork template. Fix merged.
- **Windows title bar logo compression** (PR #2316): Logo compressed with sidebar collapsed. Fix merged.

### Low
- **OpenClaw duplicate thinking messages** (PR #2324): History reconciliation caused duplicates. Fix merged.

## Feature Requests & Roadmap Signals
No new feature requests were filed today. Current development priorities visible from merged PRs suggest next release will include:
- **Windows web installer** (optional, CDN-based download)
- **Enhanced desktop notifications** (permission requests, foreground mode)
- **Improved Windows/macOS installer robustness** (self-healing, binary signing)
- **Streamed OpenClaw thinking blocks**
- **Cross-session queued follow-ups with attachments**

## User Feedback Summary
No direct user feedback (issues, comments, reactions) was recorded today. The high volume of build/installer fixes (3 PRs) and notification enhancements suggest recent field issues with Windows installation and user experience on first launch.

## Backlog Watch
Two stale PRs remain open with no recent maintainer attention:

- **#1277** (dependabot, opened 2026-04-02): Bumps `electron` from 40.2.1 to 43.1.0. This would be a major version jump — potential breaking changes. Needs review.
  - [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)

- **#1323** (stale, opened 2026-04-02): Fix cowork `input-too-long` error misclassification. Could cause misleading UX for users with short inputs. Needs review.
  - [PR #1323](https://github.com/netease-youdao/LobsterAI/pull/1323)

- **#1488** (stale, closed 2026-04-06): Scheduled task UI overhaul (card grid, search, history). Already closed but indicates this feature area has pending UX improvements.

- **#1494** (stale, closed 2026-04-06): Cowork skill selection per-session. Already closed, indicating maintainers are aware of session isolation needs.

**Note:** The two open stale PRs are both dependency/bug fixes from April that have not been addressed in over 3 months. They pose moderate risk to production stability and should be prioritized.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-07-14**.

---

## Moltis Project Digest — 2026-07-14

### Today's Overview
The project is currently in a low-activity window, with no new issues, releases, or merged pull requests in the last 24 hours. There is a single open pull request (#1147) that was updated yesterday, indicating focused work on a specific backend integration. With zero open issues reported, the project appears stable from a user-facing bug perspective, but the lack of merged PRs suggests no new code has landed today.

### Releases
**None.** No new versions were published in the last 24 hours. The most recent project release remains unchanged.

### Project Progress
**No pull requests were merged or closed today.** The only PR in the pipeline is:
- **#1147 (Open):** `fix(caldav): honor time range in list_events via server-side calendar…` — This fix addresses a significant functional bug in the CalDAV integration, where the `start` and `end` parameters were not being sent to the server. While not yet merged, this PR represents the sole advancement in the current development cycle.

### Community Hot Topics
The only active community item is the open pull request:
- **PR #1147** by *thoscut* — [Link](https://github.com/moltis-org/moltis/pull/1147)
  - **Analysis:** This PR has zero comments and zero reactions, indicating it has not yet attracted community review or discussion. The underlying need here is purely functional correctness: users expecting server-side filtering of calendar events were experiencing full calendar downloads and client-side filtering, which is a performance and reliability issue.

### Bugs & Stability
**No new bugs, crashes, or regressions were reported today.** However, the open PR #1147 directly addresses a **High Severity** bug in the CalDAV client: the `range` parameter was bound but never used, meaning the `list_events` tool ignored user-specified time windows. This is a regression of documentation vs. implementation. No fix has been merged yet, so this bug remains active in the current codebase.

### Feature Requests & Roadmap Signals
**No new feature requests were made today.** The project backlog shows no user-submitted feature proposals in the current data. The primary signal for the next version remains the CalDAV time range fix described in PR #1147, which is a bugfix rather than a feature. It is likely to be included in the next minor patch release.

### User Feedback Summary
**No new user feedback, pain points, or satisfaction data were recorded in the last 24 hours.** The absence of issues and comments suggests users are either satisfied with the current state or are not actively reporting experiences. The only implicit pain point is the CalDAV date range bug, which contradicts documented behavior and likely caused confusion for users relying on server-side event filtering.

### Backlog Watch
**No long-unanswered issues or unattended PRs require immediate maintainer attention.** The only pending item is PR #1147, which has been open for three days (since 2026-07-11) with no comments from maintainers or contributors. While not yet "long-unanswered" by conventional standards, this PR should be reviewed soon to prevent feature stagnation, especially since it resolves a documented vs. actual behavior mismatch.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-07-14  
**Generated from:** GitHub data (agentscope-ai/CoPaw / QwenPaw)

---

## 1. Today's Overview

CoPaw (QwenPaw) experienced a day of intense activity with 50 issues and 50 PRs updated in the last 24 hours, reflecting a major stabilization push following the recent v2.0.0 release. The project closed 23 issues and merged/closed 28 PRs, but a significant backlog of 22 open PRs and 27 open issues remains, indicating that while the team is responding quickly to regressions, the v2.0.0 release introduced widespread stability problems. A new patch release (v2.0.0.post1) was shipped to address several critical bugs. The most pressing concern is a cluster of related issues where context compression and tool-call management break message pairing, causing API 400 errors across multiple channels and workflows.

---

## 2. Releases

### v2.0.0.post1 — Patch Release (2026-07-13)

**Changes:**
- Bumped version to 2.0.0.post1
- Fixed: prevented browser autofill on provider search input in the console UI
- Fixed: legacy session loading issues

**Impact:** This is a minor patch release. No breaking changes or migration notes are required. However, this release does not address the most critical bugs reported (context compression tool-call pairing, missing modules, approval system issues).

**Link:** [v2.0.0.post1 Release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.0.post1)

---

## 3. Project Progress

The project made notable progress on several fronts today:

**Core Stability Fixes (Merged/Closed PRs):**
- [#6052](https://github.com/agentscope-ai/QwenPaw/pull/6052) — **fix(hint): flatten background tool hint to plain assistant message** — Resolves orphan `ToolResultBlock` that caused 400 errors when background tool calls completed after offloading.
- [#6058](https://github.com/agentscope-ai/QwenPaw/pull/6058) — **fix(tool_calls): flatten offload hint + temporarily disable broken offload mechanism** — Acknowledges the current offload mechanism is fundamentally broken and disables it to prevent cascading failures.
- [#5989](https://github.com/agentscope-ai/QwenPaw/pull/5989) — **fix: multi-layer orphan tool_result message defense** — Prevents orphaned tool_result messages from surviving across session boundaries.
- [#5935](https://github.com/agentscope-ai/QwenPaw/pull/5935) — **refactor(tool_calls): unify result pruning** — Centralizes tool result pruning logic, deprecating the previous two-layer splitting approach.
- [#6050](https://github.com/agentscope-ai/QwenPaw/pull/6050) — **fix(hint): flatten background tool hint message and yield result events on SSE stream** — Complementary fix to #6052 ensuring SSE stream consistency.
- [#6044](https://github.com/agentscope-ai/QwenPaw/pull/6044) — **fix(plugins): bridge register_tool to runtime ToolRegistry pipeline** — Fixes a regression where tools registered via API were invisible to agents at runtime.
- [#6045](https://github.com/agentscope-ai/QwenPaw/pull/6045) — **fix(console): clear message queue when a session is deleted** — Fixes a UI bug where deleting a session left stale messages in the queue.

**Governance & Security:**
- [#6054](https://github.com/agentscope-ai/QwenPaw/pull/6054) — **feat(governance): relax no-finding fallback and add global sandbox switch** — Reduces low-value approval prompts and adds a global sandbox toggle in Console.
- [#6063](https://github.com/agentscope-ai/QwenPaw/pull/6063) — **fix(governance): bridge frontend tool-guard rules into policy deep scan** — Hot-reloadable custom rules now apply to governance policy.

**Testing & Maintenance:**
- [#6061](https://github.com/agentscope-ai/QwenPaw/pull/6061) — **test(plugins): add unit tests for Ponytail Quality plugin**
- [#6065](https://github.com/agentscope-ai/QwenPaw/pull/6065) — **fix: remove dead imports, dead module, and wrong asyncio mark**
- [#6062](https://github.com/agentscope-ai/QwenPaw/pull/6062) — **perf(skills): skip redundant manifest reconciliation to prevent FD exhaustion** — Resolves a file descriptor leak (#3892) that could cause system instability.

---

## 4. Community Hot Topics

### Most Active Issues (By Comments)

1. **#5996 — `[Bug]: 2.0.0对话时会产生MODEL_EXECUTION_ERROR`** (10 comments, CLOSED)  
   [Link](https://github.com/agentscope-ai/QwenPaw/issues/5996)  
   *Analysis:* The root cause was identified: the `make_offload_hint_msg()` function creates assistant messages containing orphan `ToolResultBlock` which, when serialized by the OpenAI formatter, breaks the tool message pairing contract. This was one of the most impactful bugs and was addressed by PRs #6052, #6050, and #6058.

2. **#5961 — `[Bug]: v2.0.0版本循环执行的问题`** (7 comments, OPEN)  
   [Link](https://github.com/agentscope-ai/QwenPaw/issues/5961)  
   *Analysis:* A user reports agents getting stuck in infinite write/delete loops when using Qwen 3.7-plus. This suggests a more fundamental issue with tool call orchestration that may not be fully resolved by the tool-call pairing fixes alone.

3. **#6006 — `[Bug]: 消息队列功能没有了！急急急，望修复`** (6 comments, CLOSED)  
   [Link](https://github.com/agentscope-ai/QwenPaw/issues/6006)  
   *Analysis:* Message queue functionality was completely missing in v2.0.0. The urgency ("急急急") indicates this is a high-priority regression for users relying on queue-based workflows. Fixed via PR #6045.

4. **#5947 — `[Bug]: V2.0.0版本 MCP中禁用了某些子工具的访问,但是agent还是可以调用`** (6 comments, CLOSED)  
   [Link](https://github.com/agentscope-ai/QwenPaw/issues/5947)  
   *Analysis:* The MCP tool access control (allow/deny settings) is completely broken — denied tools are still callable by agents. This indicates a regression in the governance/approval layer.

5. **#6013 — `[Question]: V2.0.0的版本,越来越不稳定了,还不如V1.xxx的版本`** (5 comments, CLOSED)  
   [Link](https://github.com/agentscope-ai/QwenPaw/issues/6013)  
   *Analysis:* User expresses strong dissatisfaction, directly comparing v2.0.0 unfavorably to Tencent's workbuddy. This represents a general user sentiment that v2.0.0 has significant stability regressions.

### Most Active PRs (By Comment Count)

- All PRs shown in the top-20 list have `undefined` comment counts, suggesting that PR discussions are happening through GitHub reviews rather than public comments. This is common in active open-source projects.

---

## 5. Bugs & Stability

### Critical Severity

1. **Orphan Tool_Result Causes 400 Errors (Multiple Issues)**  
   - **#5996** (CLOSED), **#5960** (CLOSED), **#5962** (CLOSED), **#5986** (CLOSED), **#6034** (OPEN), **#6049** (OPEN)  
   - **Root Cause:** Context compression and scroll eviction split `tool_call`/`tool_result` pairs across message boundaries. The OpenAI API rejects sequences where a `role="tool"` message lacks a preceding `tool_calls` message.  
   - **Status:** Multiple fix PRs merged (#6052, #6050, #6058, #5989). However, #6034 and #6049 remain open, indicating the fix may not be complete or deployed to all configurations.  
   - **User Impact:** Every session with tool use eventually fails with `"Messages with role 'tool' must be a response to a preceding message with 'tool_calls'"`. Affects all channels (WeChat, Feishu, Web UI).

2. **Dream/Auto-Memory Modules Broken**  
   - **#6024** (CLOSED) — `Dream` feature fails with `ModuleNotFoundError: No module named 'agentscope.tool._builtin._scripts'`  
   - **#6012** (CLOSED) — Desktop python-runtime missing `agentscope` dependency  
   - **#5965** (CLOSED) — PyInstaller bundle missing `agentscope/tool/_builtin/_scripts/` submodule  
   - **Root Cause:** v2.0.0 refactored the project away from AgentScope, but bundled distributions still attempt to import old module paths.  
   - **Status:** All three closed, but the pattern suggests packaging issues may still exist for some deployment methods.

3. **Shell Command Timeout Silent Failure**  
   - **#5963** (OPEN) — `execute_shell_command` hard-coded at 60 seconds  
   - **#6056** (OPEN) — Background offload kills subprocess immediately  
   - **Root Cause:** Runtime 2.0 imposes a 60-second hard limit on shell commands. Longer commands are silently killed and reported as success ("offloaded to background"). The LLM-provided timeout parameter is ignored.  
   - **User Impact:** Users lose control over long-running commands with no feedback. The offload mechanism is a black hole.

### High Severity

4. **MCP Tool Access Control Broken (#5947, CLOSED)** — Denied tools are still callable.
5. **Approval System Broken (#6020, OPEN)** — Approval routing sends channel-specific prompts to wrong channel; `approval_level: OFF` does not disable all approvals.
6. **Message Queue Missing (#6006, CLOSED)** — Critical feature regression, now fixed.
7. **Skills List Limited to 20 Items (#5788, CLOSED)** — Scroll-to-load-more broken due to CSS overflow restrictions.
8. **Docker browser_use Fails (#5872, OPEN)** — Chromium exits on dbus connection failure in containers.
9. **SSH Offline & Profiles 404 (#5980, OPEN)** — Features present in v1.x are completely missing in v2.0.0.

### Medium Severity

10. **Electron CLI Broken as Root (#5979, OPEN)** — Sandbox maps real user to root, Electron refuses to run.
11. **Plugin Routes Lost on Hot-Reload (#5977, OPEN)** — HTTP routes from plugins are deleted during workspace reload.
12. **TUI Crashes on Mouse Click (#6008, OPEN)** — `AttributeError: 'NoneType' object has no attribute 'region'`.

---

## 6. Feature Requests & Roadmap Signals

### User-Requested Features

1. **CIDR Whitelist for Authentication-Free Hosts (#6048)** — A user requests support for CIDR notation in the trusted host whitelist, currently limited to specific IP addresses. *Likelihood:* High. This is a straightforward backend config change with high security value.

2. **Visual Model Fallback (#5069, OPEN PR)** — A PR adds the ability to configure a visual model as fallback for text-only LLMs, allowing image/video transcription before the main model processes requests. *Status:* Open since June 10, updated recently. *Likelihood:* Medium-High. This is a valuable feature for multimodal workflows.

3. **Improved Permission System with Tool Whitelist (#5955)** — User requests a "tool whitelist" mode where users can choose "execute once" or "add to whitelist" per tool, reducing repetitive approval prompts. *Likelihood:* Medium. The governance team is actively working on this area (see PRs #6054, #6063).

4. **AgentScope Permission System Compatibility (#5958)** — User asks whether AgentScope's Java-based permission system can be used within QwenPaw. No response from maintainers yet.

### Predicted Next Release Features

Based on active PRs and maintainer activity:
- **Unified tool result pruning** (#5935, already merged)
- **Improved governance controls** with global sandbox toggle and hot-reloadable rules (#6054, #6063)
- **Visual model fallback** (#5069) — likely to be included if reviewed
- **Ponytail Quality Plugin** (#6061) — new testing infrastructure for agent quality

---

## 7. User Feedback Summary

### Strong Dissatisfaction

- **#6013** explicitly states v2.0.0 is "less stable than v1.x" and compares it unfavorably to Tencent's workbuddy in terms of stability.
- **#6006** uses urgent language ("急急急") for missing message queue feature.
- **#6034** reports "unexpected situations" including hallucinated content (asking about AI hot topics unprompted) and frequent 400 errors.

### Pain Points

1. **Regressions from v1.x to v2.0.0** — Multiple users report features working in v1.1.12 (SSH offline, profiles, message queue) that are absent or broken in v2.0.0 (#5980, #6006, #6034).
2. **Frequent 400 Errors** — The most common complaint across issues #5996, #5960, #5962, #5986, #6034, #6049. Users cannot complete multi-turn conversations with tool use.
3. **Approval System Issues** — Users find the new permission modes confusing (#5955, #6020). "Close" mode gives too much power, "Auto" and "Smart" modes require too many approvals.
4. **MCP Tool Control Broken** — Even when tools are explicitly denied, agents can still call them (#5947).
5. **Missing Core Functionality** — Message queuing, SSH offline access, and profile pages are completely absent in v2.0.0 for some users.

### Positive Signals

- The development team is responding rapidly to critical bugs, shipping a patch release and merging multiple fixes within 24 hours.
- Several users are actively contributing fixes (niceIrene, vanwaals, nguyenthanhthe, tadebao), indicating a healthy contributor community.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Priority | Notes |
|-------|-----|----------|-------|
| [#2439](https://github.com/agentscope-ai/QwenPaw/issues/2439) — Voice message transcription broken | 108 days | Medium | Updated yesterday but still open after 3.5 months. May need maintainer triage. |
| [#5872](https://github.com/agentscope-ai/QwenPaw/issues/5872) — Docker browser_use fails | 5 days | High | Container usability is critical for server deployments. No maintainer response yet. |
| [#5963](https://github.com/agentscope-ai/QwenPaw/issues/5963) — Shell command timeout capped | 3 days | High | Hard-coded 60s limit is a significant regression. PRs #6056 and #5963 are linked but no resolution. |
| [#5980](https://github.com/agentscope-ai/QwenPaw/issues/5980) — v2.0.0 missing features (SSH, Profiles) | 2 days | High | Users on v1.x cannot upgrade without losing critical functionality. No roadmap commitment yet. |
| [#5979](https://github.com/agentscope-ai/QwenPaw/issues/5979) — Electron CLI fails as root | 2 days | Medium | Linux users running as root cannot use Electron-based tools. |
| [#6017](https://github.com/agentscope-ai/QwenPaw/issues/6017) — Internal error on API 400 kills session | 1 day | High | Whole session is killed when upstream API returns 400, with no recovery path. |
| [#6020](https://github.com/agentscope-ai/QwenPaw/issues/6020) — Approval routing & OFF mode broken | 1 day | High | Two distinct bugs in the approval system. No maintainer response. |
| [#6034](https://github.com/agentscope-ai/QwenPaw/issues/6034) — Multiple unexpected behaviors | 1 day | High | User reports hallucinated content, internal errors, and 400 errors. No maintainer response. |

### PRs Stalled

- **#5069** — Visual model fallback (open since June 10, 34 days). Updated recently but no merge. Important feature for multimodal workflows.
- **#5791** — Console formatCompact fix (open since July 5). First-time contributor. Needs review or merge.

---

## Summary Assessment

**Project Health:** 🟡 **Cautionary**

While the CoPaw (QwenPaw) team is responding to critical issues at an impressive pace, the v2.0.0 release introduced a cluster of regressions that are severely affecting user trust and workflow reliability. The most critical issue — tool-call pairing breaks causing 400 errors — has been addressed through multiple merged PRs, but open issues suggest the fix may not be comprehensive. The broken approval system, missing features, and silent shell command failures represent significant barriers to enterprise adoption.

**Key Risks:**
- User confidence is eroding, with some users explicitly stating they preferred v1.x
- Backward compatibility is not maintained for essential features (SSH, message queuing, profiles)
- The offload mechanism is acknowledged as broken and has been disabled (PR #6058), but users who rely on it have no workaround

**Positive Indicators:**
- Rapid fix turnaround (critical bugs fixed within 24-48 hours)
- Strong contributor community developing and testing fixes
- Ongoing governance improvements suggest a roadmap for production-grade security controls
- New testing infrastructure (Ponytail plugin) indicates investment in quality assurance

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-14

## Today's Overview

The ZeroClaw project shows high activity with 50 issues and 50 pull requests updated in the past 24 hours. Among issues, 34 remain open and 16 were closed, while PRs show 48 open and just 2 merged—indicating a heavy review pipeline with a pending merge bottleneck. The v0.8.3 milestone is closing out, with all six child trackers closed and only the release-closeout index remaining; the team is now shifting focus toward the SOP (Standard Operating Procedure) capability and persistent memory parity trackers. No new releases were cut today.

## Releases

No new releases were created in the past 24 hours. The latest release remains v0.8.3 (feature-frozen, in final validation). No migration notes or breaking changes to report for today.

---

## Project Progress

Two PRs were merged or closed today:
- **#9044** [CLOSED] — `google_workspace` tool rejects camelCase methods required by gws (batchUpdate). The fix corrected validation to accept camelCase method names, unblocking Google Workspace API calls.  
  [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/9044)

- **Multiple v0.8.3 child trackers closed**: The six trackers for the v0.8.3 milestone (observability/CI/docs: #8073, runtime execution: #8071, provider serialization: #8360, channel adapters: #8362, gateway/web: #8070, config routing: #8363) were all closed, signaling the feature-frozen release is near completion.

Key features advancing via open PRs include:
- **SOP (Standard Operating Procedure)** — Large PRs #8979, #9027, #8848 add deterministic pipeline building blocks: approval-gated channel gate prompts, AMQP dispatch idempotency, and per-SOP admission policies.
- **Localization** — PR #9049 adds Spanish, French, and Japanese translations for agent-scope rejection messages.
- **Memory architecture** — PRs #9041 and #9042 document the memory backend decision (ADR-005, ADR-008 canonicalization), formalizing the SQLite default with dual config options.
- **macOS release tooling** — PR #9014 adds notarization and stapling for macOS DMG offline validation; PR #9032 embeds the dashboard in the macOS release sidecar.

---

## Community Hot Topics

**Most commented issues (last 24h):**

1. **#6808** — RFC: Work Lanes, Board Automation, and Label Cleanup (14 comments)  
   *Rev 16 of a governance RFC that proposes routing work without manual overhead. Accepted and in rollout.*  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)

2. **#6165** — RFC: Prefer a lighter ZeroClaw core through external integrations (9 comments)  
   *Proposes moving long-tail integrations out of core toward skills, MCP servers, and plugins. Signals architectural tension around bloat vs. usability.*  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)

3. **#5287** — Feature: Local-First Mode for Small Models (5 comments, 2 👍)  
   *Demand for compact prompting, strict parsing, and no prompt leakage when using local models like Ollama.*  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)

**Most commented PRs (today):** None show comment counts (undefined), but large PRs #8979 (XL), #9027 (XL), and #8848 (XL) are actively discussed as SOP milestone building blocks.

**Underlying needs:** The community is focused on three themes: (1) **architectural governance** — how to keep the core lean while supporting integrations; (2) **local-first computing** — making ZeroClaw viable on small models with no prompt leakage; and (3) **deterministic SOP pipelines** — enabling approval-gated, channel-driven workflows that don't require live agent turns.

---

## Bugs & Stability

**High-severity bugs reported today:**

| Issue | Severity | Summary | Fix PR? |
|-------|----------|---------|---------|
| [#9035](https://github.com/zeroclaw-labs/zeroclaw/issues/9035) | S1 - Workflow blocked | Docker Compose gateway remains loopback-bound behind published port; "Connection refused" | No fix PR yet |
| [#9028](https://github.com/zeroclaw-labs/zeroclaw/issues/9028) | S2 - Degraded | Ctrl+C on Windows force-quits the agent (exit code 1073741510) | No fix PR yet |
| [#9046](https://github.com/zeroclaw-labs/zeroclaw/issues/9046) | S2 - Degraded | `models_cache.json` is read but never written; `/model` always returns empty | No fix PR yet |
| [#6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) | S3 - Minor | Channel runtime command replies bypass Fluent localization (hard-coded English) | No fix PR yet |

**Regression fix PRs in progress:**
- [#9040](https://github.com/zeroclaw-labs/zeroclaw/pull/9040) — Restores foreground startup feedback for `zeroclaw daemon` (lost in #7934)
- [#9029](https://github.com/zeroclaw-labs/zeroclaw/pull/9029) — Fixes OpenAI vision capability (vision returned `false` for `gpt-4o` etc.)
- [#9027](https://github.com/zeroclaw-labs/zeroclaw/pull/9027) — Fixes AMQP dispatch idempotency (duplicate SOP runs)

**CI/test stability:** Issue [#8847](https://github.com/zeroclaw-labs/zeroclaw/issues/8847) reports `cargo test --doc` failing under Rust 1.96 due to duplicated rustdoc theme flag (S3).

---

## Feature Requests & Roadmap Signals

**High-priority feature requests surfaced today:**

1. **#8998** — Dedicated GUI surface for channel pairing codes (Telegram/WeChat/Line). Users want pairing codes visible on the dashboard, not buried in logs.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/8998)

2. **#9022** — Optional Slack Events API (HTTP Request URL) mode for scale-to-zero deploys. Adds an HTTP receive path alongside the existing polling and Socket Mode.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/9022)

3. **#8997** — Config validation warning when `peer_groups.*.channel` ref points at a non-existent alias.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/8997)

4. **#9047** — Clarify ZeroCode session history vs. persistent-memory isolation. Users are confused about whether Code tab interactions write to agent memory.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/9047)

**Prediction for next release (v0.8.4):** Expect:
- **SOP milestone completion** — the dozen+ open SOP PRs suggest v0.8.4 will ship the daemon-owned SOP control plane
- **Local-first mode** (#5287) has momentum and 2 👍 — may land as a config option
- **Channel pairing GUI** (#8998) is accepted and could ship in a dot release
- **Memory separation** — RFC #9048 and ADR #9042 imply the memory separation feature is architecturally ready

---

## User Feedback Summary

**Real pain points expressed today:**

- **Docker networking confusion** (Issue #9035): "Connection refused" after `docker compose up -d` with properly bridged ports is blocking users on S1 severity.
- **Windows instability** (Issue #9028): Ctrl+C hard-crashes the agent with exit code 1073741510; users expect graceful shutdown.
- **Model catalog confusion** (Issue #9046): `zeroclaw models refresh` hint exists but does nothing—users can't see models after install.
- **Localization gaps** (Issue #6548): Chinese-language users see English strings in channel runtime replies despite `zh-CN` locale configuration.
- **Memory separation confusion** (Issue #9047): Users don't understand why Code tab interactions don't persist across sessions—"parallel interaction modes with important behavioral difference" is not documented enough.

**Satisfaction signals:** The SOP milestone is receiving heavy community contribution (multiple PRs from maintainers and external contributors), suggesting strong buy-in for deterministic pipeline features.

---

## Backlog Watch

**Issues/PRs needing maintainer attention:**

1. **#5287** — Local-First Mode for Small Models (2 👍, 5 comments, accepted since April 4). No assignee, no PR. High demand for local-model users.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/5287)

2. **#8288** — SOP milestone tracker (no stale, updated July 14). Active but the dozen+ open PRs (#8848, #8979, #9027, #9030) need review bandwidth. Several are `needs-author-action` or `needs-maintainer-review`.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/issues/8288)

3. **#8496** — Deferred-MCP access policy (opened June 29, `needs-maintainer-review`). Centralizing MCP access policy as single source of truth—stuck awaiting review.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/pull/8496)

4. **#8447** — ESP32 firmware protocol sharing (opened June 29, `needs-author-action`). The contributor may need guidance to unblock.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/pull/8447)

5. **#8353** — Error message improvements (opened June 26, `needs-author-action`). Small but stalled—author may have moved on.  
   [GitHub](https://github.com/zeroclaw-labs/zeroclaw/pull/8353)

**Project health indicator:** The 48 open PRs vs. 2 merged today suggests a review bottleneck. Maintainers should prioritize merging small, risk-low PRs to reduce queue pressure, especially the `size:XS` localization and documentation improvements.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*