# OpenClaw Ecosystem Digest 2026-07-22

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-22 01:18 UTC

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

# OpenClaw Project Digest — 2026-07-22

## 1. Today's Overview
OpenClaw shows extremely high activity with **500 issues and 500 PRs updated in the last 24 hours**, indicating a very busy development period. The project has **392 open/active issues** and **337 open PRs**, with **108 closed issues and 163 merged/closed PRs** — a healthy close rate of ~22% for issues and ~33% for PRs. No new releases were published today. The high volume of activity suggests the team is in an intensive bug-fixing and feature-development sprint, with several critical P0/P1 issues demanding attention. Security and stability remain dominant themes, with many issues tagged with security-impact labels.

## 2. Releases
No new releases were published today. The latest available release remains **2026.7.1** (referenced in Issue #106779). The most recent versions referenced across issues include `2026.6.6`, `2026.6.8`, `2026.6.9`, and `2026.7.1`.

## 3. Project Progress
Today's merged/closed activity (163 total) includes several notable fixes:
- **#102336** (CLOSED) — Fixed macOS AppKit automatic termination in menu bar app (same fix superseded by newer PR #112463)
- **#98437** (CLOSED) — MCP loopback bundle consolidated schema definition warnings — thousands of daily warnings reduced
- **#91383** (CLOSED) — Fixed Telegram reply truncation when messages begin with Markdown links
- **#95441** (CLOSED) — Fixed GitHub Copilot/gpt-5.5 `thinkingSignature` replay issue after previous fixes
- **#108178** (CLOSED) — Fixed session context tokens showing misleading "full" indicators when provider lacks usage data

Active PRs showing forward progress:
- **#112441** — Native app locale refresh (cross-platform)
- **#112353** — macOS Gateway TLS pin protection for operator traffic
- **#112458** — Forwarding selected Anthropic profiles to Claude CLI (supports OAuth/token profiles)
- **#112457** — Enforcing Claude CLI cron tool policies and MCP allowlist translation

## 4. Community Hot Topics
**Most commented issues (15+ comments):**

- **[#10659] Feature: Masked Secrets** — 15 comments, 4 upvotes. Requires system preventing agents from seeing raw API keys. High security relevance.

- **[#101290] CLI preflight corrupts live state DB** — 13 comments, P0 regression. "Database disk image is malformed" on macOS. Critical stability issue.

- **[#86996] Active Memory + Codex causes latency/stalls** — 11 comments, 2 upvotes. Complex interaction between memory backends and OpenAI/Codex models causing gateway event-loop stalls.

- **[#85030] MCP tools not injected into subagents** — 11 comments, 5 upvotes (highest reaction count). Subagents receive only built-in tools, ignoring `bundle-mcp` and allowlist configurations.

- **[#106779] Issue with 2026.7.1** — 11 comments. Local llama.cpp provider fails with parser generation error on macOS M5 Max.

- **[#7722] Filesystem Sandboxing Config** — 10 comments, 4 upvotes. Users attempt to restrict file access but find sandboxing non-functional.

**Most active PRs by comment count (undefined shown, but by size/complexity):**

- **[#112441] Native locale refresh** — XL size, cross-platform
- **[#112353] MacOS Gateway TLS pins** — XL size, maintainer-tagged
- **[#89039] Prevent silent message loss** — XL size, P1, addresses `EmbeddedAttemptSessionTakeoverError`
- **[#102228] Install ClawHub packages** — XL size, maintainer-tagged
- **[#102296] Plan-first Claw status and remove** — XL size, feature showcase
- **[#110438] Local marketplace watches** — XL size, maintainer-tagged

**Underlying needs:** The community is strongly focused on security (secrets management, tool sandboxing, MCP isolation), reliability (DB corruption, message loss, session recovery), and local model support (llama.cpp regression). Users want better subagent tool control and more predictable session behavior.

## 5. Bugs & Stability

**Critical (P0):**
- **[#101290] CLI preflight corrupts live state DB** — "database disk image is malformed" after health-check commands. Impacts macOS 2026.6.6. Four occurrences in five days. No fix PR linked yet. Tagged as regression and stable.

**High (P1):**
- **[#86996] Active Memory + Codex path causes latency/hook timeouts/stalls** — Specific config (active-memory + honcho + lossless-claw + Codex) causes unreliability. Has 11 comments, no fix PR.
- **[#85030] MCP tools not injected into subagents** — `bundle-mcp` + allowlists all ignored. 11 comments, 5 upvotes. No fix PR.
- **[#106779] llama.cpp provider fails on 2026.7.1** — Parser generation failure, MacBook Pro M5 Max. Needs info from user.
- **[#53408] Write/exec tool parameters silently dropped** — After 15+ turns, tool parameters silently disappear. Impact: session state and message loss. No fix PR.
- **[#90840] Subagent raw output delivered instead of summary** — Regression where child raw completion goes to chat user. Fix PR exists at [#89287](https://github.com/openclaw/openclaw/pull/89287) (ready for maintainer look).
- **[#111498] Main agent blocked by workspace-state migration** — macOS regression after Anthropic auth recovery. No fix PR.
- **[#108473] Cron tool schema breaks llama.cpp tool-calling** — Regex pattern issue. No fix PR.
- **[#95612] cli-backend agent returns 401 with Anthropic** — Identical claude invocation works in shell. No fix PR.
- **[#88562] models.json generator writes apiKey as plain string** — Security regression: secrets written as plain text instead of secret-ref objects. No fix PR.

**Existing fix PRs for bugs:**
- **#89287** (ready for maintainer) — Fixes subagent completion delivery target verification
- **#89039** (XL, P1) — Prevents silent message loss from retry/session-lock race conditions
- **#105806** — Fixes stuck-session recovery for terminal-phase reply operations
- **#105884** — Fixes Vydra media generation request policy leaks
- **#103823** — Guards subagent orphan recovery against concurrent double-resume
- **#109076** — Fixes Discord webhook send hangs
- **#111636** — Prevents Zalo Bot API request hangs

## 6. Feature Requests & Roadmap Signals

**High-priority requests likely in next version:**
1. **[#10659] Masked Secrets** (P1, diamond lobster) — Critical for enterprise adoption. Would prevent prompt injection credential extraction.
2. **[#20786] Telegram Business Bot support** (P2, 6 upvotes) — Growing demand for business message handling.
3. **[#7722] Filesystem Sandboxing Config** (P2, diamond lobster) — Essential for multi-tenant deployments.
4. **[#16670] Onboarding wizard with Memory setup** (P2) — Users missing critical memory configuration during setup.
5. **[#84527] Antigravity CLI (agy) support** (11 upvotes, highest) — Google Gemini CLI deprecation requires migration to `agy`.

**Pipeline signals:**
- **Session management features** (snapshots #13700, save/load, export/import #13616) suggest growing enterprise needs
- **Cost tracking** (#13219) and per-model usage logging indicate operational maturity
- **Permission manifests** (#12219, #12678) show security architecture evolution
- **Capability-based tool permissions** (#12678) would enable safe multi-agent deployments
- **Plugin hot-reload** (#14438, 4 upvotes) addresses developer experience pain

## 7. User Feedback Summary

**Pain points expressed by users:**
- **"API keys are exposed to agents"** — [#10659] Users worry about credential leakage through prompt injection
- **"Database keeps corrupting"** — [#101290] Four DB corruptions in five days on macOS, no clear root cause
- **"llama.cpp broke after update"** — [#106779] Update 2026.7.1 broke local model support on Apple Silicon
- **"MCP tools don't work in subagents"** — [#85030] Tool allowlists and MCP bundles ignored entirely
- **"Tool parameters silently disappear"** — [#53408] Long conversations lose tool arguments without error
- **"Can't use basic features without embedding config"** — [#16670] Setup wizard omits memory configuration
- **"Group chats force separate sessions"** — [#7524] No `groupScope: "main"` equivalent for consolidated experience
- **"Subagent announcements can't be suppressed"** — [#8299, #13911] No config for suppressing sub-agent output

**User satisfaction signals:**
- High engagement (500 issues, 500 PRs active) indicates strong community investment
- Users filing detailed bug reports with reproduction steps shows technical sophistication
- Multiple agent-generated reports (#95441, etc.) show users automating bug reporting via OpenClaw itself
- Feature requests include thoughtful configuration proposals with example YAML/JSON

## 8. Backlog Watch

**Long-unanswered important issues needing maintainer attention:**
- **[#7722] Filesystem Sandboxing Config** (P2, created Feb 3, 10 comments) — 5+ months old. Diamond lobster severity. Users attempted implementation but hit unspecified roadblocks.
- **[#16670] Onboarding Wizard with Memory Setup** (P2, created Feb 15, 9 comments) — 5 months. Diamond lobster. Critical UX gap.
- **[#7472] (not shown but related)** — Security review needed on several issues dating to February 2026
- **[#7524] GroupScope consolidation** (P2, Feb 2) — 5 months, 5 comments. Feature request with 4 upvotes.
- **[#6599] /models test-fallback command** (P3, Feb 1) — 5.5 months. 6 comments. Useful operational tool.

**Long-open high-severity issues (P1, 3+ months):**
- **[#86996] Active Memory latency** — Created May 26, 11 comments. System-wide impact.
- **[#85030] MCP subagent injection** — Created May 21, 11 comments. Core functionality broken.
- **[#20786] Telegram Business Bot** — Created Feb 19, 9 comments. Platform feature gap.

**Stale issues with linked PRs still open:**
- **[#48373] feishu_doc create silently ignores content** (P2, Mar 16) — Linked PR open, needs review
- **[#13219] Per-model usage logging** (P2, Feb 10) — Linked PR open, security review needed

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Analysis — 2026-07-22

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing a **massive surge in development velocity**, with the five most active projects collectively processing over 700 issues and 800 PRs in a single day. The landscape is bifurcating: established players like OpenClaw and IronClaw are undergoing major architectural rewrites (IronClaw's Reborn, OpenClaw's session/memory consolidation), while newer entrants like NanoBot and ZeroClaw are racing to close feature gaps and fix stability regressions. A clear **security-first theme** dominates—every major project has critical bugs involving credential exposure, sandbox bypass, or data integrity. The ecosystem is moving from experimental prototypes toward production-grade infrastructure, with enterprise needs (secrets management, multi-tenancy, audit trails) now driving roadmap priorities across nearly every project.

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release | Health Score | Activity Tier |
|---------|---------------------|-------------------|-------------|--------------|---------------|
| **OpenClaw** | 500 | 500 | None (2026.7.1 latest) | ⚠️ Moderate | **Very High** |
| **IronClaw** | 41 | 50 | **v1.0.0-rc.1** (Jul 20) | ✅ Good | **Very High** |
| **ZeroClaw** | 50 | 50 | None | ⚠️ Moderate | **Very High** |
| **CoPaw** | 41 | 50 | **v2.0.1-beta.1** (today) | ✅ Good | **High** |
| **NanoBot** | 11 | 33 | None | ✅ Good | **High** |
| **Hermes Agent** | 50 | 50 | None (v0.19.0 latest) | ⚠️ Stressed | **Moderate-High** |
| **LobsterAI** | 1 | 10 | None | ✅ Good | **Moderate** |
| **NanoClaw** | 1 | 12 | None | ✅ Good | **Low-Moderate** |
| **PicoClaw** | 8 | 8 | None (v0.3.1 latest) | ⚠️ Mixed | **Low-Moderate** |
| **NullClaw** | 0 | 0 | None | N/A | **Inactive** |
| **TinyClaw** | 0 | 0 | None | N/A | **Inactive** |
| **Moltis** | 0 | 1 (bot) | None | ✅ Stable | **Maintenance** |
| **ZeptoClaw** | 0 | 0 | None | N/A | **Inactive** |

**Health Notes:**
- **OpenClaw**: High absolute activity but only 22% issue closure rate and 33% PR merge rate suggest bottlenecked review pipeline
- **ZeroClaw**: Two S0 security bugs, 5 large PRs stalled on `needs-author-action`
- **Hermes Agent**: 2 P1 bugs with no fix PRs, backlog growing faster than closure rate (6:1 open-to-closed ratio)
- **PicoClaw**: Stale high-priority security dependency (vodozemac replacement unaddressed for 43 days)

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Community scale**: 500 daily updates dwarfs all competitors—OpenClaw has roughly 10x the activity volume of the next most active project. This network effect attracts more contributors and faster bug discovery.
- **Release maturity**: Shipping versioned releases (currently 2026.7.x) with consistent cadence, while IronClaw pre-RC and ZeroClaw/CoPaw are still in beta cycles.
- **Model provider breadth**: Issues mention gpt-5.5, Claude, Gemini, llama.cpp, and Anthropic—wider provider support than any single competitor.
- **MCP ecosystem leadership**: First to implement loopback bundle schemas, MCP allowlist translation, and subagent tool injection (though buggy—see #85030).

**Technical Approach Differences:**
- **Monolithic core + plugin architecture**: Unlike IronClaw's Rust-based Reborn rewrite or NanoBot's lightweight modular design, OpenClaw maintains a Python-based monolithic core with extensive plugin/MCP extensibility.
- **Session complexity**: OpenClaw's session management is the most feature-rich (context tokens, live state DB, workspace-state migration) but also the most bug-prone, with P0 DB corruption and session contamination issues.

**Community Size Comparison:**
- OpenClaw's 500 daily issues/PRs ≈ 12x NanoBot (33), 10x Hermes (50), and 10x CoPaw (41)
- However, IronClaw's 90 combined issues+PRs represent a *higher per-developer throughput* given a smaller core team
- ZeroClaw matches OpenClaw's volume (100 combined/day) but with lower closure rates

## 4. Shared Technical Focus Areas

| Focus Area | Projects Affected | Specific Requirements |
|------------|-----------------|----------------------|
| **Secrets Management** | OpenClaw (#10659), NanoBot (#5010, #4803), IronClaw (#4545), ZeroClaw (#9240) | Masked credentials, env-var vs plaintext, atomic config writes |
| **Tool/Subagent Isolation** | OpenClaw (#85030, #7722), ZeroClaw (#8279, #9247), Hermes (#25083) | Sandboxing, allowlist enforcement, workspace boundaries, immutable skills |
| **Session Reliability** | OpenClaw (#101290), ZeroClaw (#8642, #8731), CoPaw (#6299, #6241) | DB corruption, memory leaks, context contamination, zombie processes |
| **Provider Compatibility** | OpenClaw (#106779), NanoBot (#4934), CoPaw (#6257), ZeroClaw (#8615) | llama.cpp regressions, Qwen thinking leaks, tool call formatting, think tag stripping |
| **MCP Tool Registry** | OpenClaw (#85030), Hermes (#67187), ZeroClaw (#8642) | Subagent injection, server re-registration, schema cloning OOM |
| **Autonomous Sessions** | ZeroClaw (#8303), IronClaw (#6263), OpenClaw (#86996) | Goal/bounded mode, memory backends, lossless state persistence |
| **Multi-Platform Channels** | NanoClaw (#3096), PicoClaw (#3255), ZeroClaw (#8505), CoPaw (#6281) | LINE support, DingTalk preview, Telegram configuration, mobile web UI |
| **Observability** | NanoBot (#4867), IronClaw (#6439), ZeroClaw (#9248), CoPaw (#6183) | Prompt caching telemetry, eval harnesses, log rotation, run-history receipts |

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | ZeroClaw | NanoBot | Hermes | CoPaw |
|-----------|----------|----------|----------|---------|--------|-------|
| **Primary Language** | Python | Rust | Python | Python | Python | Python |
| **Architecture** | Monolithic core + MCP plugins | Reborn: Rust runtime + Web UI | Plugin-based with SOP engine | Lightweight, skill-oriented | Desktop + TUI + Gateway | Desktop + Feishu/WeCom |
| **Target User** | Power users, developers | Enterprise ops, developers | Developers, autonomous agents | Hobbyists, quick starters | Individual power users | Enterprise (China market) |
| **Unique Strength** | Largest ecosystem & model support | First production-grade Rust runtime | Goal-mode autonomous sessions | Smallest footprint, fastest setup | Desktop app polish | East Asian enterprise integrations |
| **Key Weakness** | Review pipeline bottleneck | Pre-v1.0 stability | Security maturity | Feature depth | Windows stability | V2.0 regression debt |
| **Release Cadence** | Monthly (versioned) | RC phase (rapid) | No stable release yet | Patch releases | Monthly | Beta phase |
| **Community Model** | Open contribution (500/day) | Core team + selective contributions | Balanced (50/day core + community) | Small but active | Moderate, contributor-friendly | Core team driven |

**Notable Differences:**
- **IronClaw** is the only project pursuing a Rust rewrite—all others remain Python-based. This positions IronClaw for higher performance and safety guarantees but slows feature velocity during the migration.
- **ZeroClaw** uniquely targets "bounded autonomous sessions" (goal mode)—no other project has this as a first-class feature. This is both a differentiator and a source of complexity (5+ XL PRs in flight).
- **CoPaw/AgentScope** is the only project with explicit **governance tooling** (`@tool_descriptor`, plugin defaults) and the only one deeply integrated with Chinese enterprise platforms (Feishu, DingTalk, WeCom).
- **Hermes Agent** differentiates with a **desktop + TUI** first experience—the only project offering a native desktop app as the primary interface, closest to the commercial Claude Desktop experience.

## 6. Community Momentum & Maturity

### Tier 1: High Velocity, Pre-Production
- **IronClaw** — Most organized momentum. The Reborn rewrite with v1.0.0-rc.1, coordinated epic tracking (#2987), and systematic store consolidation shows mature engineering discipline. Risk: RC quality still rough (dogfooding sprint #6394 active).
- **OpenClaw** — Highest raw velocity but lowest closure efficiency. The 500/500 daily churn suggests either massive community or bot activity. Risk: review bottleneck could burn out maintainers.

### Tier 2: Rapid Iteration, Beta/Stabilizing
- **ZeroClaw** — Fastest feature addition velocity (goal mode, OpenAI endpoint, eval harness) but accumulating security debt (2 S0 bugs). Risk: adding features faster than hardening.
- **CoPaw** — Released v2.0.1-beta.1 today, actively fixing v2.0 regressions. Good balance of fixes and features. Risk: v2.0 overhead regression (#6307) could frustrate existing v1.x users.
- **NanoBot** — High fix throughput (22 PRs merged in 24h), excellent closure rate. Smallest scope but best execution. Minimal risk—stable trajectory.

### Tier 3: Maintenance / Low Activity
- **Hermes Agent** — Active but stressed. 6:1 open-to-closed ratio, 2 P1 bugs unfixed, Windows stability cluster. Risk: backlogs growing faster than resolution.
- **LobsterAI** — Stable, incremental improvements. Focused on artifact sharing UX and cowork. Low risk, low velocity.
- **NanoClaw** — Steady but small. 12 PRs/day with focus on container fixes and East Asian channel support. Healthy for its size.
- **PicoClaw** — Mixed signals. Responsive to critical bugs (OAuth, Antigravity) but security dependency (vodozemac) languishes. Risk: stale critical deps.

### Tier 4: Inactive / Dormant
- **NullClaw, TinyClaw, ZeptoClaw** — No activity detected. May be abandoned or in deep hibernation.
- **Moltis** — Active only via Dependabot. Effectively in maintenance-only mode.

## 7. Trend Signals

### Security as Table Stakes
Every active project has bugs involving **credential leakage, sandbox bypass, or data integrity**. This is no longer a "nice to have"—masked secrets, workspace enforcement, and atomic config writes are becoming baseline requirements for any production deployment. Expect to see **permission manifests** and **capability-based tool access** become standard in the next 6 months across all projects.

### MCP Ecosystem Consolidation
Multiple projects (OpenClaw, Hermes, ZeroClaw) are investing in **MCP tool registry reliability**—subagent injection, server re-registration, schema cloning. The MCP protocol is becoming the universal integration layer, but its implementation quality varies widely. Projects that stabilize MCP tool lifecycle management will have a significant advantage.

### Autonomous Session Demand
ZeroClaw's goal mode and OpenClaw's session management investments signal a clear user desire for **agents that pursue multi-turn objectives without manual supervision**. This is the most significant feature trend beyond basic chat. Expect IronClaw and CoPaw to follow within 2-3 releases.

### East Asian Market Growth
CoPaw's Feishu/WeCom focus and NanoClaw's LINE support reflect **growing adoption in East Asian enterprise markets**. PicoClaw's Chinese-language integration fixes also point here. This is a distinct ecosystem branch—projects targeting this market must support different platforms (WeCom, DingTalk, LINE, Feishu) and handle CJK text rendering issues.

### From Chat to Platform
The emergence of OpenAI-compatible endpoints (ZeroClaw #8486), plugin SDKs (Hermes #68306), and channel APIs (multiple projects) signals that AI agents are **evolving from standalone chat apps into platforms**. Projects that build extensible integration layers will capture more ecosystem value than those optimizing the chat experience alone.

### Performance Pressure
Prompt caching (NanoBot #4867), fixed per-turn overhead (CoPaw #6307), and unbounded RSS growth (ZeroClaw #8642) show that **latency and memory efficiency are becoming competitive differentiators**. As users deploy agents for real work, sub-second turn time and 24/7 uptime become requirements, not aspirations.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for **2026-07-22**.

---

## NanoBot Project Digest — 2026-07-22

### 1. Today's Overview

NanoBot shows **very high activity**, with 33 PRs and 11 Issues updated in the last 24 hours. The project closed **22 PRs** (merged or closed) and **9 Issues**, indicating strong momentum in fixing bugs, shipping features, and addressing community concerns. There are **no new releases** today. While no single discussion is extremely long (max 22 comments), the breadth of work—spanning security, stability, provider support, and WebUI improvements—suggests the team is in an aggressive cleanup and feature-completion phase. Two open **priority: p0** and several **priority: p1** items remain active, signaling some critical items still in flight.

### 2. Releases

**No new releases** were published today.

### 3. Project Progress

The following major pieces of work were **merged or closed** today:

- **Tool Result Integrity (#4663):** Merged a fix to quarantine invalid/duplicate/missing tool results before provider replay and session persistence, resolving a long-standing protocol repair bug (#4058).
- **Security Documentation (#5010):** Updated `SECURITY.md` to recommend environment variable references over plaintext API keys, with a note that `chmod 600` is a secondary option.
- **ModelScope Provider (#4965):** Added ModelScope as a built-in provider via its OpenAI-compatible API endpoint, supporting Qwen, DeepSeek, Kimi, GLM, MiniMax, and others.
- **WebUI Polish:** Merged smart highlighting of `$skillname` references in sent messages (#5020) and a simplified `hidden_settings_sections` config option (#4399) to reduce UI noise for non-technical users.
- **Provider & Encoding Fixes:** Merged sanitization of UTF-16 surrogates at the provider request boundary (#4952), cron schedule field coercion from string to int (#4983), atomic config file writes (#4984), and environment variable resolution for transcription API keys (#4989).
- **Exec Security:** Merged a fix to the shell workspace guard’s absolute-path extraction regex to catch paths after `=` signs (#4594), and merged a fix to log suppressed `prepare_call` exceptions instead of swallowing them silently (#4811).

### 4. Community Hot Topics

The most active discussions this period reveal strong user focus on **performance**, **tool protocol reliability**, and **model integration**:

- **Prompt Prefix Caching (#4867, 22 comments, closed):** A user reported that NanoBot adds ~60 seconds per turn with Ollama because it fails to preserve the exact prompt prefix for KV-cache reuse. The community and developers discussed caching strategies and model-agnostic prompt engineering. *Outcome:* Closed as resolved, likely via a provider-side fix.
- **Endless <tool_call> Loop (#4864, 4 comments, 1 👍, open):** A gateway bug where the `complete_goal` tool misparses a JSON `recap` parameter as a bare string, causing the agent to retry endlessly. User reports this is a regression from a recent serialization change. *Outcome:* Open; fix likely coming.
- **Guarded Tool Gateway Seam (#4911, 1 comment, 1 👍, closed):** A request for a channel-level mechanism to run the agent's tools (e.g., for real-time voice). This was merged, indicating the team is investing in multi-modal channel architectures.
- **User Confirmation for Shell Execution (#5013, 1 comment, closed):** A Chinese-speaking user requested a human-in-the-loop confirmation before executing shell commands in WebUI. Closed, likely with a feature PR in the pipeline.

### 5. Bugs & Stability

The following bugs were reported or fixed today, ranked by severity:

- **[P0] Endless Goal Loop & Workspace Bypass (#5022, #4987):** An open `priority: p0` fix for workspace checks being bound to file handles (using `O_NOFOLLOW`), and a new `priority: p1` fix adding `/cancel-goal` to break sustained-goal loops. Both address deep architectural reliability issues.
- **[P1] Qwen Thinking Content Leak (#4934, open):** Qwen models expose internal `thinking/reasoning` content in chat responses, creating a poor user experience. A PR (#5023) is open to add Qwen model-level thinking style mapping.
- **[P1] File Read OOM (#4785, closed):** Fixed `read_file` loading entire multi-GB files into RAM before truncation. Fix was merged (likely as part of #4987).
- **[P1] Unbounded Message List (#4787, closed):** Fixed `Session.messages` growing without bound, even though display cap existed. Fix merged.
- **[P1] Child Process Orphans (#4794, closed):** Fixed exec sessions not cleaning up child processes on shutdown. Fix merged.
- **[P1] Tool Runner Catches KeyboardInterrupt (#4788, closed):** Fixed `AgentRunner._run_tool()` catching `BaseException`, which masked Ctrl+C and `SystemExit`. Fix merged.
- **[P1] UTF-16 Surrogates (#4952, closed):** Fixed emoji-heavy messages causing `UnicodeEncodeError` at the provider boundary. Fix merged.
- **[P1] Void Transcription API Key (#4989, closed):** Fixed env-var interpolation not applied to transcription paths. Fix merged.

### 6. Feature Requests & Roadmap Signals

Several feature requests and PRs point to the likely direction of the next NanoBot release:

- **Model Presets Bound to Sessions (#4866, open):** Allows persistence of per-session model overrides (e.g., a user picks a model for a conversation and it sticks). Likely to ship in the next minor version.
- **Skill Reference Highlighting (#5020, closed):** Already merged; next WebUI release will highlight `$skillname` references in sent messages.
- **Codex Fast Mode (#5019, closed):** Added support for OpenAI Codex Fast mode via `service_tier: "priority"`. Likely shipping.
- **Qwen Thinking Style Fix (#5023, open):** If merged, this will fix the Qwen thinking content leak for all non-DashScope providers.
- **Explicit Skill Context Loading (#5018, open):** Allows direct callers to preload specific skills; currently ignored in the system prompt. This is a lower-priority enhancement but signals deeper API flexibility.
- **Shell Execution Confirmation (#5013, closed):** A human-in-the-loop middleware for shell commands is planned, likely via the existing WebUI channel.

**Prediction for next release:** Expect a **0.7.x** release that includes: Qwen thinking fix, model presets per session, WebUI skill highlighting, and the cumulative security/stability fixes from the past week.

### 7. User Feedback Summary

- **Satisfaction:** Users are actively contributing high-quality bug reports and PRs. The closed issues show a responsive maintainer team. The ModelScope provider addition (#4965) saw community engagement and was merged quickly.
- **Pain Points:**
  - **Prompt caching with Ollama (#4867):** 60-second-per-turn overhead is cited as "totally unusable." The fix was closed but users may need to verify it works for their setup.
  - **Qwen thinking leak (#4934):** A visible annoyance for Qwen users, especially on non-DashScope providers.
  - **Security concerns (#4803, #5010):** API keys stored in plaintext caused one user to file a detailed security report. Mitigated by documentation updates and the atomic config fix.
  - **Tool regression (#4864):** The `complete_goal` tool mis-parsing JSON caused a goal loop. Users feel the recent gateway change broke their workflows.
- **Voice/Transcription Users:** Notable frustration with transcription failing due to env-var interpolation issues (#4989), now fixed.

### 8. Backlog Watch

The following items remain **open** with no recent maintainer response or no assigned milestone, requiring attention:

- **PR #4399 — Hidden Settings Sections (open since June 18):** A `priority: p1` feature for WebUI simplification. Despite being open for over a month, it has a `conflict` label and no merge. Likely blocked on WebUI refactoring.
- **PR #4594 — Shell Guard Equals Sign (open since June 29):** A security fix for path extraction after `=`. Closed today? (It appears on this list but may have been merged—if not, it needs re-review).
- **Issue #4058 — Tool Result Protocol Repair (closed, but root cause):** The fix was merged (#4663), but the underlying protocol design may still need a broader architectural review.
- **Issue #4864 — Endless Goal Loop (open):** No fix PR yet; user reports it as a recent regression. Needs maintainer prioritization.

---

**Summary:** NanoBot is in a healthy state with high contributor activity, strong focus on security and stability, and a clear roadmap toward better WebUI and provider features. Two priority-zero bugs remain open, and the Qwen thinking leak continues to affect users. All other critical bugs filed this week have been closed, demonstrating good turnaround.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-22

## Today's Overview

Hermes Agent shows **moderate to high development activity** today with 50 issues and 50 PRs updated in the last 24 hours. The open-to-closed ratio is approximately 6:1 for both issues (43 open vs 7 closed) and PRs (43 open vs 7 merged/closed), indicating a healthy pipeline of work in progress but a growing backlog of open items. **No new releases** were published today; the project remains on v0.19.0 across its components. The community is actively reporting bugs and requesting features, with **two P1 (critical) severity bugs** filed today—one involving worker deadlocks and another involving SQLite database corruption during desktop updates. Several high-quality fix PRs have been submitted to address the most serious issues, suggesting responsive maintainer engagement.

## Releases

**No new releases today.** The latest version remains v0.19.0 (desktop) and v0.18.x (agent core). Users migrating to v0.19.0 should be aware of the Windows `state.db` zeroing bug reported today (see Bugs & Stability).

## Project Progress

Seven PRs were merged or closed today (7 of 50 updated):

- **#68997** *(CLOSED)* — `fix(windows): share one bounded, tree-killing git probe across both probe call sites` — A critical Windows fix that resolves `subprocess.run` deadlocks on Windows by implementing a tree-killing strategy with bounded `communicate()` calls after timeout. Supersedes two prior attempts (#68622, #66038).
- **#68896** *(CLOSED)* — `fix(tests): anchor MCP breaker opened_at to monotonic now, not a literal` — Kills a CI-only flake in MCP circuit-breaker tests where hardcoded timestamps collided with fresh CI runner boot times.
- **#67187** *(CLOSED)* — Bug fix for MCP parked server revival that didn't re-register tools (community-reported).
- **#38786** *(CLOSED)* — Bug fix for Hermes Desktop showing `[Image blocked: ...]` for locally generated images on Windows.
- **#54675** *(CLOSED)* — Security fix for multiplexed gateway where secondary profiles used the default profile's bot token (P2 security boundary).
- **#65677** *(CLOSED)* — MCP server connection failure fix for 'jules' and 'thunderbird' stdio servers.
- **#62212** *(CLOSED)* — MCP stdio keepalive probe infinite reconnect loop fix.

Feature PRs still open and advancing include:
- **#60417** — `/behavior` command with 5-axis behavioral analysis (P3, open since July 7)
- **#68306** — TUI widget-app SDK with three reference apps (P3, open since July 21)
- **#46366** — Cron run statistics (elapsed time + token usage) appended to output (P3, open since June 15)
- **#62993** — Major security hardening pass across TLS, XML, tarfile, shell injection, and dependency CVEs (P2, open since July 12)

## Community Hot Topics

### Most Active Issues (by comment count):

1. **#47349** — *"Feature: Configurable Memory Backends"* (13 comments, 1 👍)
   - Proposes renaming `memory.md` → `rules.md` and making memory backends configurable (disable file-based, use honcho/fact_store only). **Hidden need:** Users want Hermes to support external/structured memory stores and decouple from hardcoded file injection. The 13 comments suggest significant user interest in memory system flexibility.

2. **#25083** — *"Feature: Immutable/protected skills"* (7 comments, 0 👍)
   - Requests the ability to mark skills as read-only to prevent the agent from modifying critical governance/safety rules. **Hidden need:** Power users deploying Hermes as an autonomous agent need safety guarantees that their foundational skills won't be overwritten.

3. **#67187** — *"[Bug]: MCP: parked server revival reconnects but does not re-register tools"* (7 comments, CLOSED)
   - A confirmed MCP tool registry bug where reconnected servers don't expose their tools. **Now fixed.**

4. **#64900** — *"[Feature]: Allow plugins to extend send_message with platform-specific schema fields"* (5 comments)
   - Users want to add custom parameters (voice selection, structured metadata) per platform without editing core code. **Hidden need:** The plugin architecture needs to be more extensible for platform-specific features.

### Most Active PRs:
- **#68997** (Windows git probe fix) — merged rapidly, superseding earlier attempts
- **#68899** — `fix(compression): prevent stale-budget retry loops` — addresses a compression death spiral, high interest from maintainers
- **#68994** — Copilot ACP hardening + Cursor provider fallback — significant cross-provider work

## Bugs & Stability

### P1 (Critical) Bugs:
| Issue | Component | Description | Fix PR? |
|-------|-----------|-------------|---------|
| **#68915** | Agent, Cron, Terminal | Worker deadlocks when agent backgrounds a server via shell `&` (orphaned subshell holds stdout pipe open) — **permanent Python-level deadlock** | Not yet |
| **#68474** | Desktop, Windows | `state.db` zeroed (95MB of null bytes) during desktop update to v0.19.0 on Windows — pre-update snapshot preserved | Not yet |

### P2 (High) Bugs:
| Issue | Component | Description | Fix PR? |
|-------|-----------|-------------|---------|
| **#68920** | Desktop/TUI | Active-session leases accumulate in `active_sessions.json`, eventually blocking new sessions | Not yet |
| **#68858** | Agent, Gateway | v0.19 in-place compaction + dual FTS maintenance saturates disk I/O, wedges gateway shutdown | Not yet |
| **#68979** | Desktop | Long-thread reconciliation re-stacks recent user messages after context compression (visual-only) | Not yet |
| **#68895** | Desktop | Orphaned composer queue entries cause permanent error notifications across restarts | Not yet |
| **#68943** | CLI | Removed API providers not truly removed from models list | Not yet |
| **#68944** | CLI, MCP | `hermes mcp add` silently absorbs `--env` into `--args` | Not yet |
| **#68911** | Gateway | Gateway force-redacts standalone E.164 phone numbers with no opt-in | Not yet |
| **#68990** | TUI | Thai combining marks dropped/doubled during streamed rendering (stored content correct) | Not yet |

### Fix PRs in Progress:
- **#69019** — fix(desktop): stop long-session transcript from drifting to old turns (regression from `9b8b054c2`)
- **#68899** — fix(compression): prevent stale-budget retry loops (compression death spiral)
- **#68766** — fix(agent): recover sessions on transient provider outages (#33693)
- **#69002** — fix(tui-gateway): fail closed on session reasoning scope
- **#69010** — fix: distinguish kanban capacity backpressure from dispatcher stalls
- **#69012** — fix(gateway): require explicit delivery acknowledgement for kanban notifications
- **#69013** — fix(oneshot): discover explicitly requested MCP toolsets before agent build
- **#69017** — fix(kanban): enforce idempotency keys atomically
- **#68999** — fix(ui-tui): widget-grid hardening — review fast-follow for #20379

### Windows-Specific Issues:
A notable cluster of Windows-specific bugs persists:
- **#68474** — state.db corruption during update
- **#68997** (now fixed) — git probe deadlocks
- **#64685** — fflate import + RDP GPU fallback (PR open)

## Feature Requests & Roadmap Signals

### Likely to Ship in v0.20.0 (based on PR activity):
- **Per-function tool filtering** (#68964) — finer-grained control than toolset-level enable/disable
- **Searchable timezone dropdown** in Desktop Settings (#68970)
- **Atomic Hermes (mobile) as send_message target** (#68951)
- **Plugin-extensible send_message** (#64900) — platform-specific schema fields

### Strategic Signals:
1. **Memory system redesign** (#47349) — renaming `memory.md` → `rules.md` and supporting configurable backends could be a v0.20 or v1.0 milestone feature
2. **Protected/immutable skills** (#25083) — essential for production/enterprise deployments where agent self-modification is a liability
3. **Behavioral analysis** (#60417) — the `/behavior` PR suggests Hermes is moving toward providing users with qualitative insights about their agent usage patterns, not just quantitative metrics
4. **TUI widget SDK** (#68306) — significant platform expansion, making the TUI a first-class app development surface

## User Feedback Summary

### Pain Points (Explicitly Stated):
- **Windows stability** — Multiple Windows-specific bugs: git deadlocks (now fixed), state.db corruption during updates, Electron renderer crashes under RDP
- **SQLite corruption under load** — Two separate kanban DB corruption issues (#34385, #53819) from concurrent multi-process writes; users are hitting this in production with high concurrency
- **MCP tool registration fragility** — Parked servers failing to re-register tools (#67187, now fixed); keepalive infinite reconnect loops (#62212, now fixed)
- **Desktop session management** — Leaking session leases (#68920), orphaned composer queues (#68895), transcript drift (#68979) — the desktop UX has a cluster of session-state bugs
- **Configuration deletion persistence** — Deleting API providers doesn't actually remove them from model lists (#68943)

### Satisfaction Signals:
- **Rapid bug fixing** — Multiple MCP tool registry bugs were identified and closed within days
- **Positive community engagement** — Users filing detailed bug reports with root cause analysis and reproduction steps
- **Feature demand is sophisticated** — Users are asking for enterprise-grade features (immutable skills, fine-grained tool permissions, structured memory backends)

## Backlog Watch

### Issues Needing Maintainer Attention (unanswered or languishing):

1. **#34385** (May 29) — *"Kanban DB index corruption under concurrent multi-process access in WAL mode"* — 5 comments, `needs-decision`. Despite a confirmed root cause report, this remains open with no assigned fix. Duplicate #53819 (June 27) also open. **This is the longest-standing unresolved P3 bug and could be a P2 given real-world concurrency impact.**

2. **#23207** (May 10) — *"how to use web search/fetch using ollama search feature"* — 3 comments, `question`. User asking for Ollama-native web search integration. Only one maintainer comment. **Over 2 months unanswered for a straightforward feature request.**

3. **#53819** (June 27) — *"kanban DB corruption under high concurrent-worker load"* — 3 comments, `needs-decision`. This is the duplicate of #34385; both remain unresolved despite confirmed root cause. Workers need per-write serialization.

4. **#61042** (July 8) — *"TUI: /compress should allow type-ahead"* — 3 comments, P3. Feature request that would significantly improve TUI UX but has no maintainer engagement.

5. **#63413** (July 12) — *"openai-codex: pool credential never recovers from ~/.codex/auth.json"* — 1 comment, P3. Provider credential management failure with no assigned resolution path.

6. **#65868** (July 16) — *"Hermes desktop v0.17.0 crashes repeatedly in Rust→V8 IPC bridge"* — 2 comments, P3. SIGTRAP crashes on macOS; affected user reports no workaround. **Despite being a crash bug, it's only rated P3 and has minimal engagement.**

### Stale PRs Needing Review:
- **#46366** (June 15) — Cron run statistics — open 37 days, no maintainer review comments
- **#62993** (July 12) — Security hardening pass — open 10 days, no maintainer review despite marking multiple `sweeper:risk-security-boundary` areas
- **#60417** (July 7) — Behavioral analysis — open 15 days, no maintainer review

---

*Generated from GitHub data snapshotted at 2026-07-22. All links are to NousResearch/hermes-agent.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-22

**Source:** github.com/sipeed/picoclaw | **Analysis period:** Last 24 hours

---

## 1. Today's Overview

PicoClaw shows **moderate development activity** with 8 issues and 8 PRs updated in the last 24 hours. The project maintains a healthy balance: 4 open issues, 4 closed issues, 5 open PRs, and 3 merged/closed PRs. Notably, two **high-impact bugs** surfaced today—a Google OAuth compliance failure (#3278) and a critical regression in the Antigravity provider (#3274)—both receiving swift response with dedicated fix PRs. The community continues to file thoughtful bug reports and infrastructure improvements, though some older issues remain in a "stale" state awaiting maintainer attention. No new releases were cut today.

---

## 2. Releases

**No new releases** in the last 24 hours. The latest tagged version remains **v0.3.1**, with `main` at commit `85dcfcc`.

---

## 3. Project Progress

**Merged/closed PRs today (3 items):**

- **#3282 — `feat(nodes): add policy-gated system exec`** (by bogdanovich, merged 2026-07-21)  
  This significant feature adds `system.exec.v1` to the "slim node companion," enabling controlled execution of canonical system commands without a shell. It enforces strict security boundaries: companion-owned executables, working-root isolation, environment controls, timeouts, and output limits. This is a major step toward safe sandboxed execution for the Nodes subsystem.

- **#3233 — `Fix pr 3222 backward compat`** (by yaotukeji, merged 2026-07-21)  
  A compatibility fix ensuring backward-compatible behavior for changes introduced in PR #3222. The closed status was set to "stale," suggesting a smooth merge after review.

- **#303 — `fix: make bot greeting name configurable via bot_name setting`** (by AtharvaGurao, closed 2026-07-21)  
  This older PR (created February 2026) was finally resolved. It fixes hardcoded "PicoClaw" greetings in Telegram and DingTalk by introducing a configurable `bot_name` field, addressing a long-standing customization limitation.

---

## 4. Community Hot Topics

**Most active issue:**  
[#3088 — **Feature: Use vodozemac instead of libolm**](https://github.com/sipeed/picoclaw/issues/3088)  
*9 comments, 2 👍 | Status: Open, stale, priority: high*  
The community strongly advocates replacing `libolm` (unmaintained, insecure) with `vodozemac`, the official Matrix replacement library. This issue has been open since June 9 and carries a high-priority label, yet no PR has materialized. The lack of movement despite clear security implications is a signal that Matrix security hardening may be under-resourced.

**Most commented PR (recent):**  
No PRs with explicit comment counts in the data, but the following generated significant discussion indirectly via their linked issues:
- [#3280 — **fix(auth): make browser OAuth login survive real-world callback conditions**](https://github.com/sipeed/picoclaw/pull/3280) (by honbou, open 2026-07-21)  
  Directly addresses two critical authenticated issues (#3274, #3278), representing the day's most urgent infrastructure work.

**Key community concern under debate:**  
The **OAuth ecosystem** is under active discussion, with users reporting that Google has begun enforcing stricter OAuth policies against PicoClaw's client configuration. Multiple issues and PRs today circle the same frustration: authentication flows that break in "real world" headless/remote deployments.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#3278](https://github.com/sipeed/picoclaw/issues/3278) | **Google OAuth login blocked**: "doesn't comply with Google's OAuth 2.0 policy for keeping apps secure." New Google policy enforcement is blocking all Antigravity provider auth. | Fix PR [#3280](https://github.com/sipeed/picoclaw/pull/3280) submitted same day |
| **Critical** | [#3274](https://github.com/sipeed/picoclaw/issues/3274) | **Antigravity INVALID_ARGUMENT regression**: Tool schema transform `"simple"` no longer sufficient on `main` branch (v0.3.1 was fine). Crashes API calls. | Being addressed in same PR #3280 |
| **High** | [#3281](https://github.com/sipeed/picoclaw/issues/3281) | **Web UI input laggy with long history**: Chat input becomes unusably slow with moderate conversation length. | No fix yet (0 comments, filed today) |
| **High** | [#3255](https://github.com/sipeed/picoclaw/issues/3255) | **DingTalk preview shows "PicoClaw" instead of content**: Chat list preview always shows fixed bot name, not the actual reply message text. | No dedicated fix PR; partially addressed by #303 |
| **Medium** | [#3203](https://github.com/sipeed/picoclaw/issues/3203) | **Matrix sync loop dies silently**: No reconnection after network/server disruption. Process stays alive so `Restart=on-failure` doesn't trigger. | No fix PR (open 19 days) |
| **New fix** | [#3279](https://github.com/sipeed/picoclaw/pull/3279) | **Tool-call format leak in seahorse summaries**: Fix for `partsToReadableContent` converting tool-call formats to readable text. Open PR. | PR open, 0 comments |

**Notable regression**: The Antigravity provider tool schema issue (#3274) is a **classic build-from-source regression** — the user was on `main` @ `85dcfcc`, where `tool_schema_transform "simple"` is no longer sufficient, yet no migration guidance was provided for the breaking change.

---

## 6. Feature Requests & Roadmap Signals

**Top requested features:**

1. **#3088 — Replace libolm with vodozemac** (Open 43 days, priority: high)  
   Security-critical dependency upgrade. The stale label suggests it's been de-prioritized despite 'high' priority. *Likely in next major release.*

2. **#3200 — Configurable default fallback chain** (PR open 21 days)  
   Community member `lc6464` is building backend+Web UI support for setting default model fallback chains. Large PR with persistence API. *Likely v0.4.0 candidate given size.*

3. **#3153 — Volcengine Doubao tool-call leakage** (Closed, but underlying problem)  
   Users of Chinese AI providers (Volcengine/Doubao) experience tool-call formatting bugs. The community desire for broad provider support is clear.

**Roadmap signals:**
- **Security-first direction**: The system.exec policy-gating (#3282) and OAuth fixes show maintainers prioritizing security infrastructure.
- **Anthropic caching**: PR #3228 (SystemParts + cache_control for Anthropic) indicates corporate/enterprise users pushing for prompt caching support.
- **DingTalk/Feishu polish**: Multiple PRs from Chinese community members (MrTreasure, AaronZ345) suggest strong enterprise adoption in East Asian markets, driving channel-specific improvements.

---

## 7. User Feedback Summary

**Pain points expressed:**
- **OAuth fragility**: "almost every headless / remote setup" fails (issue author [honbou] described four independent causes in one OAuth flow). Users running PicoClaw on headless servers/cloud VMs are severely impacted.
- **Silent failures**: Matrix sync dies without any log signal (#3203); "main process stays alive, systemd doesn't recover." Users are losing connectivity without knowing.
- **Rate limiting confusion**: "I only set `agents.defaults.model_name` and don't set any fallback models. This model's rpm config doesn't work" (#3232). Configuration design is non-obvious for new users.
- **UI performance**: Long chat history makes Web UI input "very laggy" (#3281). Single-input-box slowness suggests missing virtualization/memoization.

**Positive signals visible:**
- Multiple contributors stepping up with code (bogdanovich, honbou, MrTreasure, lc6464, AayushGupta16) — healthy contributor community.
- Detailed, well-formatted bug reports (structured environment sections, reproduction steps) indicate a technically sophisticated user base.
- Chinese-language integration issues (DingTalk, Feishu) are being actively fixed, suggesting strong and growing adoption in that region.

---

## 8. Backlog Watch

| Item | Age | Status | Maintainer Attention Needed |
|------|-----|--------|---------------------------|
| [#3088 — vodozemac replacement](https://github.com/sipeed/picoclaw/issues/3088) | 43 days | Open, stale, high priority | **Yes** — Security dependency; stale label contradicts priority; needs assignment or roadmap comment |
| [#3203 — Matrix reconnection](https://github.com/sipeed/picoclaw/issues/3203) | 20 days | Open, 4 comments | **Yes** — Critical Matrix channel stability issue; no PR exists; users losing connectivity silently |
| [#3255 — DingTalk preview](https://github.com/sipeed/picoclaw/issues/3255) | 8 days | Open, stale | **Low** — Cosmetic UX issue; PR #303 partially addresses the root cause in a different area |
| [#3228 — Anthropic cache_control](https://github.com/sipeed/picoclaw/pull/3228) | 16 days | Open, stale | **Moderate** — No comments from maintainers; blocks enterprise caching use cases |
| [#3200 — Fallback chain UI](https://github.com/sipeed/picoclaw/pull/3200) | 21 days | Open | **Moderate** — Large, well-scoped feature; no review activity; risk of bit-rot |

**Most at-risk item:** Issue #3088 (vodozemac) — with no tagged release since v0.3.1 and the stale label, the project may be carrying an insecure dependency for extended periods.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — July 22, 2026

## 1. Today's Overview
Project activity is **moderately high** with 12 pull requests updated in the past 24 hours, signaling sustained community and core-team engagement. Three PRs were merged or closed, while nine remain open, reflecting a healthy but slightly backlogged contribution pipeline. One new open issue proposes adding LINE as a communication channel, indicating continued community interest in platform expansion. No new releases were published today. Overall, the project is progressing steadily with a focus on bug fixes, infrastructure hardening, and documentation improvements.

## 2. Releases
No new versions were released in the past 24 hours. The latest release remains the previous stable build; no migration notes or breaking changes to report.

## 3. Project Progress
Three pull requests were closed or merged today:

- [#3116 – sync pr](https://github.com/nanocoai/nanoclaw/pull/3116) — A guideline-compliant synchronization PR, likely a bot-driven or backlog-clearing merge.
- [#3114 – Langfuse tracing skill pr](https://github.com/nanocoai/nanoclaw/pull/3114) — Merged: a new utility skill integrating Langfuse observability/tracing into NanoClaw, enhancing debugging and monitoring capabilities.
- [#3095 – docs: rewrite branch maintenance guide for the registry-branch model](https://github.com/nanocoai/nanoclaw/pull/3095) — Closed: documentation overhaul aligning the branch maintenance guide with the current registry-branch workflow, improving contributor onboarding.

These merges advance the project's observability tooling and developer documentation quality.

## 4. Community Hot Topics
The single open issue [#3096 – feat: Add /add-line skill for LINE Official Account channel support](https://github.com/nanocoai/nanoclaw/issues/3096) has attracted **3 comments** and is the most-discussed item. The author proposes adding LINE, a dominant messenger in Japan, Taiwan, and Thailand, as a supported channel. The issue notes that no `@chat-adapter/line` package exists yet, implying a need for either package development or adapter contribution. This reflects strong community demand for East Asian messaging platform support.

No PRs have accumulated significant comment threads today; most remain at 0 comments, suggesting focused, low-controversy submissions.

## 5. Bugs & Stability
Several bug-fix PRs are active, with no critical regressions reported in the last 24 hours. Ranked by severity:

- **High (with fix PR):** [#3113 – fix(whatsapp): stage inbound media where the container can read it](https://github.com/nanocoai/nanoclaw/pull/3113) — Addresses a container-scoped file system issue where WhatsApp media cannot be read by the process, causing inbound media delivery failures.
- **Medium (with fix PR):** [#2236 – fix(container): align WORKDIR with actual group mount path](https://github.com/nanocoai/nanoclaw/pull/2236) — A long-standing container configuration bug where the Docker `WORKDIR` points to an empty artifact directory instead of the agent's workspace, causing execution context issues.
- **Low (with fix PR):** [#2896 – fix(whatsapp): apply media-failure note at the inbound boundary](https://github.com/nanocoai/nanoclaw/pull/2896) — Follow-up fix for a regression where approval-answer paths could bypass media-failure notifications.
- **Infrastructure (with fix PR):** [#1530 – fix: add SELinux :z label to Docker volume mounts](https://github.com/nanocoai/nanoclaw/pull/1530) — Blocks Docker execution on SELinux-enforcing hosts (Fedora, RHEL); open since March but updated today, suggesting renewed attention.

Additionally, PR [#3115 – fix(onecli): block legacy Gmail API routes](https://github.com/nanocoai/nanoclaw/pull/3115) proactively prevents Gmail traffic from bypassing newer API endpoints via legacy paths, improving reliability for email integrations.

## 6. Feature Requests & Roadmap Signals
The most prominent feature signal is **LINE channel support** ([#3096](https://github.com/nanocoai/nanoclaw/issues/3096)), which if merged, would expand NanoClaw's reach into the East Asian market. The author explicitly cites the README's "Request for Skills" process, indicating this follows the project's intended community-driven roadmap.

Additional signals:
- [#3112 – docs(claude): note OneCLI/system-Postgres port collision and fix](https://github.com/nanocoai/nanoclaw/pull/3112) — Documents a real-world installation pitfall (PostgreSQL port 5432 collision), suggesting a future fix may be needed to make `onecli setup` more robust on hosts with existing Postgres installations.
- [#3050 – feat(setup): add Dial to the channel picker + wizard/skills](https://github.com/nanocoai/nanoclaw/pull/3050) — Adding Dial as a new channel, another sign of expanding messaging integrations.

Likely inclusions in the next version: Dial channel support, LINE channel support, and the Langfuse tracing skill (already merged).

## 7. User Feedback Summary
Indirect user pain points expressed through contributions:
- **Installation friction:** PR [#3112](https://github.com/nanocoai/nanoclaw/pull/3112) documents a real-world port collision between OneCLI's bundled Postgres and system Postgres, highlighting a usability issue for developers who already run databases locally.
- **Platform gaps:** Issue [#3096](https://github.com/nanocoai/nanoclaw/issues/3096) from a user in Taiwan (as implied by the Traditional Chinese README contribution) underscores the need for East Asian messaging support. The same author contributed [#2950](https://github.com/nanocoai/nanoclaw/pull/2950) (Traditional Chinese README), showing localized community investment.
- **Container reliability:** Multiple PRs (#2236, #3113, #1530) address container-scoped bugs that cause silent failures or permission issues, indicating that container deployment is a common but friction-prone use case.

No explicit negative satisfaction signals were observed; the community appears engaged and constructive.

## 8. Backlog Watch
Several important PRs have remained open for extended periods without maintainer merge/closure action:

- [#1530 – fix: add SELinux :z label to Docker volume mounts](https://github.com/nanocoai/nanoclaw/pull/1530) — **Opened March 29, updated today** (114 days open). This is a high-impact fix for Fedora/RHEL users, yet stalled for over three months. The update today suggests it may finally be under review.
- [#2236 – fix(container): align WORKDIR with actual group mount path](https://github.com/nanocoai/nanoclaw/pull/2236) — **Opened May 3** (80 days open). A straightforward container configuration fix that affects anyone using Docker volumes.
- [#2896 – fix(whatsapp): apply media-failure note at the inbound boundary](https://github.com/nanocoai/nanoclaw/pull/2896) — **Opened June 30** (22 days open). A follow-up to a merged PR, meaning the regression it fixes is live in the current version.
- [#3050 – feat(setup): add Dial to the channel picker](https://github.com/nanocoai/nanoclaw/pull/3050) — **Opened July 14** (8 days open). A feature skill that may be waiting for review against channel-addition criteria.
- [#2950 – docs: add Traditional Chinese README](https://github.com/nanocoai/nanoclaw/pull/2950) — **Opened July 4** (18 days open). A documentation-only PR that is low-risk and would improve international accessibility.

**Recommendation:** Maintainers should prioritize #1530 and #2236 to resolve long-standing container compatibility issues, and review #2896 to prevent a live WhatsApp regression from persisting.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-22

## Today's Overview

The IronClaw project is in an intense **pre-v1.0.0 stabilization and architecture consolidation phase**, driven by the Reborn architecture rewrite that has been in progress since late April 2026. Activity is extremely high: **41 issues** and **50 PRs** updated in the last 24 hours, with 14 issues closed and 17 PRs merged/closed in that window alone. The first release candidate (`ironclaw-v1.0.0-rc.1`) landed on July 20, marking a major milestone — this is a **ground-up rebuild** of the agent runtime, storage, extension host, and web UI, not an incremental update. The project is now heavily focused on **witness-based dispatch consolidation, store cleanup (removing in-memory stores), error recoverability hardening, and test infrastructure expansion** to ensure the v1.0.0 release is production-ready. Several core contributors and the CI bot are driving simultaneous PRs across architecture, dependencies, and QA, indicating a coordinated push toward release.

## Releases

**New Release: `ironclaw-v1.0.0-rc.1`** (2026-07-20)  
[GitHub Release](https://github.com/nearai/ironclaw/releases/tag/ironclaw-v1.0.0-rc.1)

This is the **first release candidate** of the completely rearchitected IronClaw v1.0.0. It is **not** an increment on the 0.29.x line — it is a ground-up rebuild of:
- Agent runtime
- Storage layer
- Extension host
- Web UI

The `ironclaw` binary now ships as the rearchitected CLI monolith. Key notes:
- **Breaking changes are expected** — this is a new architecture replacing legacy v1/engine v2 paths
- The release notes only cover the beginning of the RC; additional detail is expected as the release stabilizes through the current sprint
- Projects should test migration from 0.29.x with caution; the Reborn architecture introduces new runtime service profiles, credential injection, and capability policy systems

The release channel will likely see additional RC iterations (rc.2, rc.3) based on the volume of open issues and PRs.

## Project Progress

**Merged/Closed PRs Today (17 total):** Significant architecture consolidation occurred:

**Architecture & Store Consolidation:**
- **PR #6430** ([closed](https://github.com/nearai/ironclaw/pull/6430)) — Removed in-memory ratchet store allowances, migrating durable cases to filesystem-backed stores. This eliminates a major tech-debt category tracked in issues like **#6263** (InMemoryTurnStateStore retirement)
- **PR #6432** ([closed](https://github.com/nearai/ironclaw/pull/6432)) — Completed witness-always-present and origin→gate matrix portions of the authority dispatch system; routes sealed mounts/reservations through the new witness system. Partially addresses **#6396**
- **PR #6116** ([closed](https://github.com/nearai/ironclaw/pull/6116)) — Merged unified generic extension runtime + Option A honest state machine reconciliation (92 commits from main)

**Dependency & Security Updates:**
- **PR #6196** ([closed](https://github.com/nearai/ironclaw/pull/6196)) — Bumped dompurify from 3.2.3 to 3.4.11 (XSS sanitization fix)

**Open PRs Advancing Today (33 open):**

| PR | Type | Focus |
|----|------|-------|
| [#6442](https://github.com/nearai/ironclaw/pull/6442) | refactor | Unify runtime store graph selection, replace production runtime services with composite root filesystem |
| [#6441](https://github.com/nearai/ironclaw/pull/6441) | refactor | Name `ProductSurface` boundary trait over frozen `RebornServicesApi` facade |
| [#6436](https://github.com/nearai/ironclaw/pull/6436) | refactor | Sole-witness dispatch input + HIGH review fixes missed in #6432 merge |
| [#6438](https://github.com/nearai/ironclaw/pull/6438) | feat | Seal process redispatch authority — persist `ProcessAuthorizedContinuation` |
| [#6437](https://github.com/nearai/ironclaw/pull/6437) | fix | Make model-visible failures recoverable — rout failures through typed recovery paths |
| [#6439](https://github.com/nearai/ironclaw/pull/6439) | test | Replay all 42 harvested QA traces with Emulate.dev mock-LLM adapter |
| [#6425](https://github.com/nearai/ironclaw/pull/6425) | fix | Restore SSE streams across navigation in WebUI |
| [#6422](https://github.com/nearai/ironclaw/pull/6422) | test | Harvest full per-case LLM trace catalog from live-QA runs |
| [#6365](https://github.com/nearai/ironclaw/pull/6365) | feat | Per-user hosted-MCP discovery (worker agents with connector tools) — reference PR by new contributor |
| [#5563](https://github.com/nearai/ironclaw/pull/5563) | feat | Design system tokens + /playground for WebUI v2 |

## Community Hot Topics

**Most Active Issues (by comment count):**

1. **#2987** ([open](https://github.com/nearai/ironclaw/issues/2987)) — **[EPIC] Track Reborn architecture landing strategy and grouped PR plan** (44 comments)
   - The parent epic for the entire Reborn migration. Last updated 2026-07-21 with landing shape updates. This remains the single most important tracking issue for the project's direction
   - *Need:* Coordinated delivery of a massive architecture rewrite without overwhelming reviewers with single giant PRs

2. **#6263** ([closed](https://github.com/nearai/ironclaw/issues/6263)) — **§4.3 final store consolidation: retire InMemoryTurnStateStore** (10 comments)
   - The last DEBT entry for removing in-memory stores. Resolved today via PR #6430
   - *Need:* Production-grade persistence replacing development-only in-memory stores

3. **#6389** ([open](https://github.com/nearai/ironclaw/issues/6389)) — **Phase 4 (§5.11): collapse build_local_runtime + build_production_shaped into one build_runtime(cfg)** (10 comments)
   - Active technical discussion about unifying two runtime-assembly paths
   - *Need:* Simplified, single configuration path for runtime deployment

4. **#2767** ([closed](https://github.com/nearai/ironclaw/issues/2767)) — **Epic: Separate engine v2 capability background from callable tool schemas** (7 comments)
   - *Need:* Clean separation between LLM capability descriptions and actual tool execution schemas for engine v2

5. **#3036** ([open](https://github.com/nearai/ironclaw/issues/3036)) — **[EPIC] Configuration-as-Code for IronClaw Reborn** (7 comments, 1 👍)
   - *Need:* Declarative configuration with schema, diff, audit trail for operators

6. **#3031** ([open](https://github.com/nearai/ironclaw/issues/3031)) — **[EPIC] Reborn product surface migration** (7 comments)
   - *Need:* Preserve existing user/operator behavior during the Reborn transition

**Most Active PRs:**

- **#6361** ([open](https://github.com/nearai/ironclaw/pull/6361)) — Serialization group dependency update (serde + serde_json)
- **#5598** ([open](https://github.com/nearai/ironclaw/pull/5598)) — Release automation PR with breaking changes in `ironclaw_common` and `ironclaw_skills` crates

## Bugs & Stability

**New/Updated Bug Reports (today):**

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#6394](https://github.com/nearai/ironclaw/issues/6394) | **High** | **[EPIC] Dogfooding & QA bug fixing 07/20-07/24** — A dedicated sprint for bugs found during internal dogfooding of RC1 | In progress |
| [#6433](https://github.com/nearai/ironclaw/issues/6433) | **Medium** | Feature request for dedicated custom instructions UI (implies current UX gap) | No |
| [#6434](https://github.com/nearai/ironclaw/issues/6434) | **Medium** | Seal process re-dispatch — loose CapabilityDispatchRequest still exists without witness | [#6438](https://github.com/nearai/ironclaw/pull/6438) |
| [#6437](https://github.com/nearai/ironclaw/pull/6437) | **High** | Model-visible failures not recoverable — opaque executor failures block model recovery | #6437 (open) |

**Stability Observations:**
- The project is actively addressing **error recoverability** as a first-class concern (see epic #6284: "the model recovers from 100% of the errors it sees")
- PR #6432 merged today had two HIGH review fixes that raced past the merge — PR #6436 now carries those fixes
- SSE stream lifecycle in WebUI was broken across navigation (#6425 fix PR is open)
- Multiple dependency bumps are in progress, suggesting proactive maintenance of the supply chain

## Feature Requests & Roadmap Signals

**New User-Facing Feature Request:**
- **#6433** ([open](https://github.com/nearai/ironclaw/issues/6433)) — **Dedicated custom instructions / master prompt section** — User requests a ChatGPT/Claude-style dedicated UI for personalization settings, separate from chat context. This is a clear gap in the current Reborn WebUI v2 compared to competitors
  - *Prediction:* Moderate likelihood for v1.0.0-rc.2 or v1.0.0 — the request comes from `sergeiest` (first-time issue author) and touches UX, but the project is prioritizing architecture consolidation

**Development-Facing Features Being Actively Worked:**
- **Per-user hosted-MCP discovery** (PR #6365) — Worker agents with connector tools, by new contributor `kirikov`. Reference/draft PR for porting
- **Design system tokens + /playground** (PR #5563) — WebUI v2 design system so AI can implement small improvements autonomously
- **Harness testing unification** (epic #2828) — Unifying replay, E2E, live canary, and eval coverage into a single framework

**Predictions for Next Release (v1.0.0-rc.2 likely within 1-2 weeks):**
- Witness-based dispatch fully rolled out (closing #6396)
- In-memory stores completely removed (already underway)
- Reborn product surface migration reaching "compatibility gate" (#3020 status to watch)
- QA trace replay infrastructure merging (#6439 is open today)

## User Feedback Summary

Based on issues and PRs, user/operator pain points:

1. **Onboarding/Setup Difficulty** — Epic #4533 explicitly calls out that "Reborn cannot replace V1 as the operational binary until users and operators can set it up, inspect it, debug it, and manage local service lifecycle without manually editing internal files"
2. **Missing Custom Instructions UI** — Issue #6433: users want a persistent master prompt section (like ChatGPT/Claude) rather than feeding instructions into each chat
3. **Approval Workflow Gaps** — Epic #4539: Reborn lacks full V1 approval parity (approve once, deny, always-allow for matching tool calls)
4. **Secret Management** — Epics #4545 and #5261: users need self-serve secret setup for their own tools without exposing values to LLMs
5. **Configuration Complexity** — Epic #3036: operators want declarative config-as-code with schema validation and audit trails

**Satisfaction Indicators:**
- High contribution velocity from both core team and new contributors suggests strong community engagement
- The Reborn architecture is receiving substantial investment, indicating long-term commitment
- Active dependency management (multiple dependabot PRs today) suggests good maintenance hygiene

**Dissatisfaction Indicators:**
- The pre-v1.0.0 state is clearly still rough — the dogfooding bug sprint (#6394) and multiple "HIGH review fixes missed" situations suggest quality assurance gaps
- New contributors face a rapidly evolving codebase with 57/54 divergence on reference PRs (#6365)

## Backlog Watch

**Issues Needing Maintainer Attention:**

| Issue | Created | Days Open | Status Concern |
|-------|---------|-----------|----------------|
| [#2987](https://github.com/nearai/ironclaw/issues/2987) | 2026-04-27 | 86 days | Parent epic for entire Reborn migration — still open with ongoing updates. Not a concern per se, but signals the migration has been in progress for nearly 3 months |
| [#3036](https://github.com/nearai/ironclaw/issues/3036) | 2026-04-28 | 85 days | Configuration-as-Code epic — has 1 👍 but no recent child-issue PRs; may be deprioritized post-v1 |
| [#2355](https://github.com/nearai/ironclaw/issues/2355) | 2026-04-12 | 101 days | Persistent multi-identity browser automation via Chrome + CDP — oldest non-epic enhancement open. The Reborn rewrite may have consumed resources; watch for post-v1 pickup |
| [#2392](https://github.com/nearai/ironclaw/issues/2392) | 2026-04-13 | 100 days | Host-level multi-account support for messaging channels — blocking WeCom and other channel deployments. Needs attention post-v1 |
| [#2828](https://github.com/nearai/ironclaw/issues/2828) | 2026-04-22 | 91 days | Harness testing unification epic — actively being worked but the epic itself is aged |

**Open PRs Needing Review:**
- **#5503** ([open](https://github.com/nearai/ironclaw/pull/5503)) — Google extension capabilities enhancement, opened 2026-07-01 (21 days old). Experimental; may be awaiting architecture decisions
- **#5563** ([open](https://github.com/nearai/ironclaw/pull/5563)) — Design system tokens + /playground, opened 2026-07-02 (20 days old). Blocked on design leadership feedback resolution
- **#5598** ([open](https://github.com/nearai/ironclaw/pull/5598)) — Release automation PR with breaking changes in two crates, opened 2026-07-03 (19 days old). May be waiting for RC1 stabilization before proceeding

**Note:** The 50 PRs updated in the last 24 hours indicate that the core team is actively reviewing and advancing work, so the backlog is likely being actively managed — these items are flagged for visibility rather than neglect.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-07-22**.

---

## LobsterAI Project Digest — 2026-07-22

### 1. Today's Overview
The project shows a **high-activity day** driven by the engineering team, with 10 pull requests updated in the last 24 hours (5 merged/closed) and significant focus on **bug fixes in the cowork (browser co-browsing) and artifact modules**. The community-facing activity was lower, with only 1 open issue updated, indicating that the current cycle is heavily weighted toward quality-of-life improvements and infrastructure cleanup rather than new feature development. Three stale dependency update PRs continue to languish with no maintainer response, suggesting a potential bottleneck in the update pipeline. No new releases were cut today.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress (Merged/Closed PRs)
Five PRs were merged or closed today, focusing on stability and UI polish:
- **#2372 (CLOSED)** — *Fix/openclaw token proxy SSE truncation*: A fix for the OpenClaw token proxy to address SSE (Server-Sent Events) response truncation, important for stream reliability.
- **#2371 (CLOSED)** — *fix(cowork): 完善浏览器注释内容与会话状态*: Enhances the cowork (browser annotation) system to support annotations without comments, display original-to-new value changes in prompts, and fix session state leaks when clearing drafts.
- **#2370 (CLOSED)** — *fix(artifacts): 统一分享与部署订阅拦截弹窗*: Unifies the subscription gate UI for artifact sharing and local service deployment, improving the UX flow and separating share creation from deployment.
- **#2369 (CLOSED)** — *fix(artifacts): 优化分享访问权限提交流程*: Refines the access permission submission flow for artifact sharing, adding explicit "Create Share" and "Update Permissions" actions and preventing auto-creation of shares on dialog open.
- **#2368 (CLOSED)** — *feat(update): install Windows updates silently*: Implements silent, elevated Windows NSIS installer updates with proper error handling for UAC declines (exit code 1223).

*Key takeaway:* The team is aggressively closing out PRs related to the **artifact sharing UX** and **cowork annotation synchronization**.

### 4. Community Hot Topics
The most active community discussion remains issue **#1861**, which has been open for 85 days and received recent attention:
- **#1861 [OPEN] — 图片附件不随模型切换重新处理 (Photo attachments do not re-process on model switch)**
  - Updated: 2026-07-21 (last activity)
  - URL: [Issue #1861](https://github.com/netease-youdao/LobsterAI/issues/1861)
  - **Analysis:** This is a core UX consistency bug. Users report that image attachments retain stale data (base64 vs file path) when switching between vision and non-vision models (e.g., from glm-5.1 to Doubao-Seed-2.0-lite), causing visual models to not see images. **This issue has a fix PR open today**: PR #2373 (yaodong-shen) directly addresses this by syncing attachments with model capability.

### 5. Bugs & Stability
**High Severity:**
- **Image attachment state not synced on model switch (Issue #1861)** — Users reported two scenarios (vision→non-vision and vice versa) where attachments become incorrect. **Fix in progress:** PR #2373 "fix(cowork): sync image attachments with model capability" was opened today to address this exact issue.

**Medium Severity:**
- **SSE truncation in OpenClaw token proxy (PR #2372)** — A stream data loss bug that was fixed and merged today.
- **Artifacts sharing auto-creation bug (PR #2369, fixed)** — Previously, opening the share dialog would automatically create a share; now corrected.
- **Session state leak in cowork annotations (PR #2371, fixed)** — Clearing a draft annotation did not stop the webview session, leaving the app in a stale marking state.

**Low Severity:**
- **Silent Windows update failure handling (PR #2368, fixed)** — UAC cancellation now shows a localized error instead of a raw OS message.

### 6. Feature Requests & Roadmap Signals
- **Permanent ad banner toggle (PR #2374, OPEN):** A user-facing setting to permanently hide the sidebar ad banner. This merges an existing feature request (#2342) into a dedicated toggle in Settings → General. *Prediction:* Likely to be merged in the next minor release.
- **Silent Windows updates (PR #2368, merged):** This feature significantly improves the update experience for Windows users, suggesting the team is prioritizing desktop app reliability.
- **Artifact sharing subscription gating (PR #2370, merged):** The team is unifying the paywall/subscription logic for artifact sharing and deployment. This signals a continued investment in monetization infrastructure.

### 7. User Feedback Summary
- **Pain Point — Image attachment behavior:** A core user pain point is the "sticky" attachment state when switching models. Users expect attachments to be automatically re-encoded (base64) or stripped depending on the new model's vision capability. The existence of PR #2373 indicates the team is aware and responding.
- **Satisfaction — Ad banner control:** The new permanent toggle for ads (PR #2374) directly addresses user frustration with repeated ad dismissals, likely a highly welcomed change.
- **User workflow:** The artifact sharing flow was confusing—users reported shares being created accidentally. The team's timely fix (PR #2369) suggests these UX refinements are driven by real user confusion.

### 8. Backlog Watch
Three long-standing dependency update PRs remain open with no maintainer interaction for over 110 days:
- **#1279 (OPEN, Stale)** — `chore(deps-dev): bump cross-env from 7.0.3 to 10.1.0` (Created: 2026-04-02). [PR Link](https://github.com/netease-youdao/LobsterAI/pull/1279)
- **#1280 (OPEN, Stale)** — `chore(deps): bump react-dom from 18.3.1 to 19.2.4` (Created: 2026-04-02). [PR Link](https://github.com/netease-youdao/LobsterAI/pull/1280)
- **#1281 (OPEN, Stale)** — `chore(deps-dev): bump vite from 5.4.21 to 8.0.9` (Created: 2026-04-02). [PR Link](https://github.com/netease-youdao/LobsterAI/pull/1281)

*Note:* These are dependency bumps generated by Dependabot. The major version jumps (e.g., Vite 5.4 → 8.0, React 18 → 19) may require breaking change evaluation, which could explain the delay. However, the lack of any response or labeling is a risk for long-term security and maintenance.

**Additional backlog item:** Issue #1861, while now addressed by a fix PR, was unresolved for 85 days. This indicates a gap in triage speed for UX bugs that are not security-critical.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-22

## Today's Overview
Moltis experienced minimal activity in the last 24 hours, with zero open or closed issues and no new releases. A single open pull request was updated, focused purely on dependency maintenance rather than feature development or bug fixes. The project appears to be in a low-activity or maintenance phase, with no code changes or community discussions emerging today. While not a sign of decline, the lack of new issues or PRs beyond automated dependency bumps suggests the core team may be focusing on longer-term work or that the community is not actively filing feedback at this time.

## Releases
No new releases were published today. The latest available release remains unchanged from previous reports.

## Project Progress
No pull requests were merged or closed today. The only PR activity is an open, automated dependency update (PR #1161) that has not yet been reviewed or merged. No features, fixes, or documentation improvements advanced today.

## Community Hot Topics
The sole active item is:
- **[PR #1161: chore(deps): bump astro from 7.0.9 to 7.1.3 in /docs](https://github.com/moltis-org/moltis/pull/1161)** — An automated Dependabot pull request updating the Astro documentation dependency. It has no comments, no reactions, and zero engagement from the community or maintainers. This indicates no ongoing technical debates or urgent community concerns today.

**Analysis:** The absence of community interaction likely reflects a quiet period rather than disinterest; however, it may also signal that users are not actively testing or requiring changes in the current state of the project.

## Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The issue tracker shows zero open issues of any kind. No stability-related concerns are currently documented.

## Feature Requests & Roadmap Signals
No feature requests were submitted today. Based on the complete absence of new issues or community proposals, there are no clear signals to predict what might appear in the next release. The roadmap remains opaque from the available data.

## User Feedback Summary
No user feedback, pain points, or use-case discussions were recorded today. The lack of issues or comments means there is no new data to assess user satisfaction or dissatisfaction.

## Backlog Watch
There are no long-unanswered issues or pull requests requiring maintainer attention. The only open PR (PR #1161) was created yesterday and has not yet been reviewed, but it is a routine dependency bump and not time-critical. The backlog is effectively empty.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-22

## Today's Overview
Project activity surged to a high level on 2026-07-22, with 41 issues and 50 PRs updated in the last 24 hours. The release of **v2.0.1-beta.1** indicates active iterative development post the v2.0.0 milestone. Community engagement remains strong, with 20 open issues and 20 open PRs reflecting ongoing collaborative contribution. The project continues to address critical regressions in session management, memory, and tool call stability.

## Releases
- **v2.0.1-beta.1** was released (the 'latest-release' data points to the QwenPaw repo, as CoPaw uses the same infrastructure).
  - **Changes**: Fixed absolute import in Tauri entry point (PR #6234), bumped version, fixed `OSError` in `memoryspace._saved_tool_refs` (a memory snapshot stability fix).
  - **Breaking Changes**: None noted; this is a patch fix release.
  - **Migration Notes**: Users on v2.0.0.x should update to this beta to benefit from memory-space crash fixes.

## Project Progress
30 PRs were merged or closed today. Key advances include:
- **Governance & Safety Tooling**: PR #6190 (`fix(governance): auto-register tools via @tool_descriptor`) merged, unifying tool registration metadata. Follow-up PR #6313 (`fix(governance): refresh plugin tool defaults`) also merged, hardening the registration flow.
- **OMP Workflow Integration**: PR #5882 (`feat(omp): integrate OMP workflow modes`) closed (to-be-merged), bringing five new agent workflow modes (UltraQA, Ralph, Ultrawork, Autopilot, Team) and extended `spawn_subagent` capabilities. PR #6317 then fixes post-merge regressions.
- **Agent Configuration**: PR #6270 (`feat: support user editable agent mode`) and PR #6262 (`feat(agents): add one-click copy of agent configuration`) both merged, improving agent management UX.
- **Logging & Timestamps**: PR #6183 (configurable log rotation) and PR #6305/6309 (session timestamp timezone fixes, note: PR #6309 is open) addressed operational reliability. [Link](https://github.com/agentscope-ai/QwenPaw/pull/6183) [Link](https://github.com/agentscope-ai/QwenPaw/pull/6309)

## Community Hot Topics
- **Issue #2291** (HELP WANTED: Open Tasks) — 65 comments. A meta-issue with a curated list of community tasks (P0–P2). High activity as contributors claim tasks. [Link](https://github.com/agentscope-ai/QwenPaw/issues/2291)
- **Issue #6257** (Multiple tool calls produce identical thinking output) — 13 comments. Users report that when an agent executes multiple tool calls in one turn, each call's "thinking" block shows identical content instead of independent reasoning. This is a serious UX and correctness issue. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6257)
- **Issue #4873** (Two subagents cause infinite polling) — 5 comments. Launching two subagent background tasks simultaneously triggers rapid repeated `check_agent_task` calls, flooding LLM requests and making the task un-interruptible from Feishu. [Link](https://github.com/agentscope-ai/QwenPaw/issues/4873)
- **Issue #6297** (Drag-and-drop upload of images/PDFs/Office docs) — 4 comments. Strong user demand for rich document upload in chat, specifically for contract review workflows. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6297)

## Bugs & Stability
**High Severity**:
- **Session Context Contamination** (Issue #6299, closed): Deleted session records persist in `history.db` causing `seq` collisions and cross-session context pollution. Fixed by PR #6068 (open, addressing session-ID mismatch). [Issue](https://github.com/agentscope-ai/QwenPaw/issues/6299) [PR](https://github.com/agentscope-ai/QwenPaw/issues/6068)
- **V2.0 Fixed Overhead** (Issue #6307, open): ~2 seconds of fixed per-reply overhead in v2.0 vs v1.x, independent of model latency, caused by architectural changes in the request pipeline. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6307)
- **RemoteProtocolError: peer closed connection** (Issue #6314, closed): QwenPaw (v1.1.2) actively closed HTTP connections mid-stream, causing incomplete responses. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6314)

**Medium Severity**:
- **Memory Search Loop & Duplicate Output** (Issue #6241, closed): Agents repeating identical outputs and *memory_search* deadlock. System detects warnings but does not stop re-execution. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6241)
- **Conversation Progress Loss & Infinite Loops** (Issue #5860, closed): v2.0.0-beta.3 users report frequent context-loss and infinite answer loops. [Link](https://github.com/agentscope-ai/QwenPaw/issues/5860)
- **Plan Mode Repeated File Reading** (Issue #5759, closed): Same script file read 5 times without changes during plan mode. [Link](https://github.com/agentscope-ai/QwenPaw/issues/5759)

**Low Severity**:
- **LaTeX Rendering Failure** (Issue #6320, open): Square-root LaTeX not rendering in Docker deployment. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6320)
- **Timestamp Timezone Conversion** (Issue #6301, open): Naive UTC timestamps incorrectly treated as local time. PR #6309 (open) provides a fix. [Issue](https://github.com/agentscope-ai/QwenPaw/issues/6301) [PR](https://github.com/agentscope-ai/QwenPaw/pull/6309)

## Feature Requests & Roadmap Signals
User requests trending toward enhanced enterprise and usability:
- **Conversation-level model selection** (Issue #6318): Users want to override models per-session instead of per-agent. PR #5992 (open) implements this as opt-in. [Issue](https://github.com/agentscope-ai/QwenPaw/issues/6318) [PR](https://github.com/agentscope-ai/QwenPaw/pull/5992)
- **Mobile web console** (Issue #6281): Multiple users request responsive mobile UI for the web console. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6281)
- **Drag-and-drop file upload** (Issue #6297): High demand for uploading images and documents directly in chat. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6297)
- **Real-time clock in context** (Issue #6283): Auto-attach current time to every LLM request to avoid date confusion in old sessions. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6283)
- **Loop detection mechanism** (Issue #5657, closed): Beat to add automatic loop detection for Qwen3.6 models. PRs like #6323 (staged compaction) and merged fixes suggest this will appear in v2.0.2. [Issue](https://github.com/agentscope-ai/QwenPaw/issues/5657)

**Likely for Next Version**: Configurable tool descriptions (Issue #6286), per-session model overrides (#5992), and the QwenPaw Creator app (PR #6284, under review) are strong candidates.

## User Feedback Summary
- **Pain Points**: v2.0 upgrade overhead (Issue #6307), session contamination (Issue #6299), repeated tool call thinking (Issue #6257), and subagent infinite polling (Issue #4873) cause significant frustration.
- **Satisfaction**: Users appreciate the new governance/sandbox features (PR #5088), configurable logging (PR #6183), and agent management improvements (copy config, editable modes).
- **Use Cases**: Intensive file operations (contract review #6297, report extraction #5759), multi-subagent workflows (#4873), and day-spanning conversations (#6283) highlight real-world enterprise needs.
- **Dissatisfaction**: The overall tone in issues suggests users find v2.0 less stable than v1.x for production use, with regressions in session handling and performance.

## Backlog Watch
- **Issue #6083** (opened 2026-07-14, 3 comments): Desktop window workspace shortcut button — no maintainer response yet. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6083)
- **Issue #6273** (opened 2026-07-20, 2 comments): Unify task tracking and same-session concurrency semantics — core team raised this bug (by @rayrayraykk) but no fix PR. [Link](https://github.com/agentscope-ai/QwenPaw/issues/6273)
- **PR #5992** (opened 2026-07-12): Per-session model overrides — first-time contributor, under review but not merged; has significant user demand (Issue #6318). [Link](https://github.com/agentscope-ai/QwenPaw/pull/5992)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-22

## Today's Overview
ZeroClaw is in a period of exceptionally high development activity, with 50 issues and 50 PRs updated in the last 24 hours. The project maintains a substantial open-work backlog of 47 active issues and 41 open PRs, indicating both heavy community engagement and a growing maintenance burden. Security remains a top concern, with two critical-severity bugs reported today involving workspace boundary bypass and silent data loss from configuration writes. The daemon's goal mode feature stack is approaching completion via a large multi-PR series from contributor vrurg, while the eval harness infrastructure receives significant new capabilities from IftekharUddin. No new releases were published today.

## Releases
None.

## Project Progress
**Merged/closed PRs today:** 9 total. Key closures include:

- **#8756** [bug, runtime, tool, size:XS] `fix(tests): make media marker assertions portable on Windows` — Merged. Resolved a cross-platform test failure affecting Windows CI by matching path components instead of Unix-specific path strings. (Author: Audacity88)
- **#9120** [bug, runtime, tool:sop] `[Bug]: SOP routing evaluates switch after a false top-level when` — Closed. The SOP routing engine previously evaluated switch rules even when a top-level `when` condition was false, potentially routing through unintended ports. Fix addresses degraded behavior in the `route::resolve_next` path.
- **#7082** [enhancement, channel:mattermost] `feat(channel/mattermost): add optional WebSocket listener mode` — Closed. Adds REST-poller alternative with WebSocket mode for Mattermost channels, enabling lower-latency message delivery.

**Other notable PR advances:**
- **#8486** (OpenAI Chat Completions endpoint) — Updated. The large XL-sized PR implementing an OpenAI-compatible REST endpoint continues active development, with gateway integration progressing.
- **#8443** (Matrix single-message progress drafts) — Updated. Adds `stream_mode = "single_message"` for Matrix, enabling inline progress editing before final answer delivery.
- **#9249** (Session-backend foundation) — Opened today. Supersedes #6893, providing shared config/dispatch/async-safety plumbing for all remote session persistence backends.
- **#9248** (Eval append-only run-history receipts) — Opened today. Adds `[eval].history_dir` support for timestamped eval run receipts enabling longitudinal trend analysis.

**Closed Issues today:** 3, including #9086 (Structured Security Audit Pipeline RFC, closed after author action) and #9120 (SOP routing bug, closed with fix delivered).

## Community Hot Topics

### Most Active Issues (by comment count)
1. **#8226** (6 comments) — `[Feature]: Add typed per-agent git identity for built-in git operations` — Community discussion around adding `runtime_context` and `runtime_secrets` blocks for multi-tenancy identity management. Underlying need: operational isolation for git operations across agents.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8226

2. **#8505** (6 comments) — `[Bug]: Telegram channel cannot be configured` — High-severity blocker where `channels doctor` reports channels unconfigured despite proper setup. Users report CLI works but Telegram bot is unresponsive.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8505

3. **#8303** (4 comments) — `RFC: Goal mode for bounded autonomous session work` — Active design discussion on durable goal execution mode with start/pause/cancel/budget exhaustion lifecycle. The underlying need: users want ZeroClaw to pursue objectives beyond single turns without manual supervision.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8303

4. **#8603** (4 comments) — `RFC: OpenAI Chat Completions compatibility adapter` — Community interest in OpenAI API compatibility, enabling integrations with Open WebUI, LobeChat, LangChain, and Aider. Signal: the companion PR #8486 is already in progress.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8603

### Most Reacted Issues
- **#8303** (👍1) — Goal mode RFC received positive reaction, indicating strong user demand for autonomous session capabilities.
- **#8600** (👍1) — Per-chat model switching for multi-model providers also received a thumbs-up, reflecting desire for provider-agnostic model selection.

## Bugs & Stability

### Critical Severity (S0 — Data loss / Security risk)
1. **#9247** [OPEN] — `[Bug]: Shell Tool Workspace Boundary Bypass` — **New today.** The shell tool does not enforce workspace boundaries. Symlinks pointing outside the workspace allow shell commands to read/write arbitrary directories. No fix PR exists yet. Severity rated S0.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/9247

2. **#8279** [OPEN] — `[Bug]: delegate bypasses parent's tool allowlist` — Sub-agents can invoke tools excluded by parent policy. The `delegate` tool populates children with the unfiltered parent tool set. No fix PR observed.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8279

### High Severity (S1/S2)
3. **#8642** [OPEN] — `[Bug]: MCP/tool-schema cloning drives unbounded RSS growth` — Split from OOM tracker #5542. Tool schema cloning in the agent loop causes progressive memory growth. Marked `in-progress` but no fix PR yet.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8642

4. **#8731** [OPEN] — `[Bug]: Stdio-based MCP servers accumulating as zombie processes` — Sub-processes not reaped after timeout/close, leading to PID accumulation. Marked `in-progress`.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8731

5. **#8505** [OPEN] — `[Bug]: Telegram channel cannot be configured` — S1 severity, workflow blocked. Configuration validation fails despite correct setup. Quickstart label suggests onboarding impact.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8505

6. **#8718** [OPEN] — `[Bug]: zeroclaw config init ships a config template that its own daemon rejects` — Fresh installs get silently broken voice transcription due to incompatible config defaults. S2 severity, quickstart label.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8718

### Other Notable Bugs
7. **#9240** [OPEN] — `save_dirty silently drops every write whose map key contains a dot` — **New today.** Config writes to keys containing dots (common model IDs like `gpt-4.1`, `claude-3.5-sonnet`) silently succeed but do not persist. S2 severity.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/9240

8. **#8615** [OPEN] — `[Bug]: compatible provider silently deletes content via unconditional <think> tag stripping` — Unclosed think tags produce empty replies. S2 severity.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8615

9. **#8410** [OPEN] — `[Bug]: channel tasks need a first-class intentional no-reply outcome` — Conditional tasks with no content still send visible responses. S2 severity.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8410

## Feature Requests & Roadmap Signals

### Likely for Next Release
Based on active PRs and `status:in-progress` labels:

1. **Goal mode** (RFC #8303, PR stack #8687/#8688/#8689/#8746/#8996) — The largest active feature push. Multiple XL-sized PRs from vrurg implement goal controller, verifier, trusted tools, channel admission, daemon reload persistence, and self-resume loop fixes. Very likely to land as a major feature in the next release.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/pull/8687

2. **OpenAI Chat Completions endpoint** (RFC #8603, PR #8486) — Active development with gateway integration. Would immediately enable compatibility with LangChain, Open WebUI, Continue.dev, and Aider.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/pull/8486

3. **Eval harness enhancements** (PR #9244, #9245, #9248) — Three new PRs from IftekharUddin add memory seeding, judge calibration tooling, and run-history receipts. Indicates a test infrastructure push.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/pull/9244

4. **Session persistence foundation** (PR #9249) — Supersedes #6893, adding config/dispatch plumbing for remote session backends. Foundational infrastructure likely to unblock multiple future backends.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/pull/9249

### Pipeline Features
5. **Mixture-of-Agents virtual provider** (RFC #8568) — Allows one aggregator model to consume parallel reference model outputs. Still in RFC stage.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8568

6. **Gemini Live realtime speech channel** (RFC #8780) — Backend-agnostic realtime multimodal channel starting with Gemini. Early stage RFC.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8780

7. **SkillForge wiring** (Issue #8309) — Auto skill discovery engine is "orphaned" (wired to nothing). Community divided on finishing vs. removing.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8309

## User Feedback Summary

### Pain Points
- **Onboarding friction**: Multiple reports of broken configuration defaults (#8718), incorrect documentation (#8810, #8424 new Telegram guide needed), and channel setup failures (#8505) suggest the quickstart path has regressions.
- **Security concerns**: Two S0 bugs reported today (workspace bypass #9247, config silent drops #9240) erode trust, especially the shell tool bypass which enables arbitrary filesystem access.
- **Memory stability**: Unbounded RSS growth (#8642) and zombie MCP processes (#8731) continue to affect long-running deployments.
- **Provider compatibility**: Silent content stripping (#8615), cache issues with Bedrock Nova 2 Lite (#8720), and model ID handling in config (#9240) frustrate multi-provider users.

### Use Case Signals
- **Autonomous sessions**: Multiple users request goal/bounded session mode (#8303) for pursuing objectives without manual turn-by-turn interaction.
- **OpenAI API compatibility**: Strong demand (#8603, PR #8486) for connecting existing LLM tooling (Open WebUI, Aider, Continue.dev) to ZeroClaw.
- **Model flexibility**: Users want per-chat model switching (#8600) and mixture-of-agents patterns (#8568), indicating sophistication beyond single-model deployments.

### Satisfaction Signals
- SkillForge (#8309) and SOP milestone tracker (#8288) show sustained community investment in advanced capabilities.
- The large PR count (50 updated in 24h) indicates healthy contributor engagement and review velocity.

## Backlog Watch

### Issues Needing Maintainer Attention
1. **#8309** — `SkillForge (#144) is orphaned` — Last updated 2026-07-21, but has only 2 comments. No maintainer decision on whether to finish wiring or remove. Open since June 25 (28 days).
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8309

2. **#8396** — `RFC: Make wire protocol first-class in provider construction and onboarding` — Open since June 27 (25 days). Only 2 comments. RFC design proposal without assigned milestone or successor PR.
   🔗 https://github.com/zeroclaw-labs/zeroclaw/issues/8396

3. **#7082** — `feat(channel/mattermost): add optional WebSocket listener mode` — **Now closed**, but had languished since June 2 (49 days) before closure today. Flagging pattern of long-open feature PRs.

### PRs Requiring Author Action
- **#8486** (OpenAI endpoint, XL) — Needs author action
- **#8443** (Matrix drafts, XL) — Needs author action
- **#8746** (Goal self-resume fix, XL) — Needs author action
- **#8838** (SSE streaming fix, XL) — Needs author action
- **#8638** (SkillForge replacement, L) — Needs author action

These five large PRs all carry the `needs-author-action` label, suggesting they are stalled waiting on their authors to address review feedback. Combined, they represent significant feature work (goal mode, OpenAI compatibility, streaming stability, skills overhaul) that could be blocked by unaddressed review comments.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*