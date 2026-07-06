# OpenClaw Ecosystem Digest 2026-07-06

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-06 01:53 UTC

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

# OpenClaw Project Digest — 2026-07-06

## 1. Today's Overview

OpenClaw shows **very high activity** with 500 issues and 500 PRs updated in the last 24 hours, indicating a large and engaged contributor community. Despite high open issue volume (435 open), the project maintains a healthy **closure rate** (65 issues closed, 349 PRs merged/closed today). One new beta release shipped this period (`v2026.7.1-beta.2`) adding **OpenAI GPT-5.6 support** and external harness attachment capabilities. Overall project health is **strong but under strain** — the backlog contains multiple P0/P1 security and stability issues that have been open for months, suggesting maintainer bandwidth is a bottleneck despite active triage.

---

## 2. Releases

### v2026.7.1-beta.2 (new)
**Download:** [openclaw 2026.7.1-beta.2](https://github.com/openclaw/openclaw/releases/tag/v2026.7.1-beta.2)

**New features:**
- **OpenAI GPT-5.6 model family support** across catalog, capability, and runtime selection paths ([PR #98333](https://github.com/openclaw/openclaw/pull/98333)) — thanks @steipete-oai
- **External harness attachment:** `openclaw attach` can now launch an external harness against an existing Gateway session

**Breaking changes:** None noted.

**Migration notes:** No special migration steps required.

---

## 3. Project Progress

**Merged/closed today:** 349 PRs closed or merged, 65 issues closed.

**Notable advances:**
- **Anthropic OAuth fix** ([PR #96917](https://github.com/openclaw/openclaw/pull/96917)) — keeps OAuth callback on loopback, merged today
- **Reusable WebSocket client SDK proposal** ([Issue #49178](https://github.com/openclaw/openclaw/issues/49178)) — extract `@openclaw/gateway-client` package; still open but with maintainer review
- **Policy doctor repairs** ([PR #99700](https://github.com/openclaw/openclaw/pull/99700)) — automatic repair of required-deny tool findings, ready for maintainer look
- **iOS in-flight runs after reconnect** ([PR #100277](https://github.com/openclaw/openclaw/pull/100277)) — fixes session ownership loss on iOS background/reconnect

---

## 4. Community Hot Topics

### Most active issues (by comments):

1. **#75 — Linux/Windows Clawdbot Apps** ([link](https://github.com/openclaw/openclaw/issues/75))
   - Comments: 110 | 👍: 81
   - **Need:** Desktop platform parity — users on Linux/Windows feel left behind while macOS/iOS/Android are supported. This is the most-commented issue in the entire repo, indicating a **high-priority unmet user need**.
   - **Status:** Open since Jan 2026, labeled P2, help wanted

2. **#9443 — Prebuilt Android APK releases** ([link](https://github.com/openclaw/openclaw/issues/9443))
   - Comments: 26 | 👍: 4
   - **Need:** Users want ready-to-install APK binaries, not source compilation. Submitted on behalf of a user by an AI assistant.
   - **Status:** Open since Feb 2026, P0 with multiple security labels

3. **#92201 — Embedded runner: Anthropic thinking signatures invalid on replay** ([link](https://github.com/openclaw/openclaw/issues/92201))
   - Comments: 20 | 👍: 1
   - **Need:** Critical reliability issue — streaming thinking blocks from Anthropic intermittently fail on replay; recovery wrapper never fires due to generic error text. P1.

4. **#48788 — Centralized filename encoding utility** ([link](https://github.com/openclaw/openclaw/issues/48788))
   - Comments: 18 | 👍: 1
   - **Need:** Handle multi-byte encodings (Shift-JIS, EUC-KR, GB18030) in Content-Disposition headers across all channel adapters.

5. **#63918 — Cron agentTurn sends wrong thinking to OpenAI** ([link](https://github.com/openclaw/openclaw/issues/63918))
   - Comments: 17 | 👍: 1
   - **Need:** Cron jobs send unsupported `thinking=none` to GPT-5-nano models that require `minimal`. Causes 400 errors.

### Most reacted issue:
- **#75** (Linux/Windows apps) with **81 👍** — far ahead of any other issue

---

## 5. Bugs & Stability

### Critical (P0):

| Issue | Summary | Status |
|-------|---------|--------|
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | No prebuilt Android APK releases (release blocker) | Open since Feb |
| [#48920](https://github.com/openclaw/openclaw/issues/48920) | Live docs ahead of release — `IsolatedSessions` config ref'd but not in 2026.3.13 | Open since Mar; regression |

### High Severity (P1):

| Issue | Summary | Fix PR exists? |
|-------|---------|----------------|
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | Anthropic thinking signatures invalid on replay; recovery fails | No |
| [#98416](https://github.com/openclaw/openclaw/issues/98416) | v2026.6.11 dist missing reentrancy guard — reply session init conflicted | No |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer mode does not inject messages mid-turn for main sessions | Linked PR open |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | Bootstrap files in `agentDir` silently ignored | Linked PR open |
| [#64810](https://github.com/openclaw/openclaw/issues/64810) | Heartbeat interrupts in-progress replies in Telegram topics | No |
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | Cron jobs silently time out on sustained LLM API errors | No |
| [#54155](https://github.com/openclaw/openclaw/issues/54155) | Gateway memory leak: 389MB → 14.7GB over 4 days | No |
| [#45224](https://github.com/openclaw/openclaw/issues/45224) | Unhandled Playwright assertion crashes entire Gateway | No |
| [#69118](https://github.com/openclaw/openclaw/issues/69118) | Claude CLI sessions reset every turn in group channels | Linked PR open |
| [#47975](https://github.com/openclaw/openclaw/issues/47975) | Subagent sessions persist, main session becomes unresponsive | No |
| [#49876](https://github.com/openclaw/openclaw/issues/49876) | Cron sessions hallucinate output instead of failing cleanly | No |
| [#51396](https://github.com/openclaw/openclaw/issues/51396) | `clearUnboundScopes` strips operator scopes for non-local token-auth clients | Linked PR open |

**Security-related P1 bugs:**
- [#29387](https://github.com/openclaw/openclaw/issues/29387) — Bootstrap files silently ignored (security impact)
- [#45740](https://github.com/openclaw/openclaw/issues/45740) — gh-issues skill injects untrusted issue body into sub-agent prompts
- [#10659](https://github.com/openclaw/openclaw/issues/10659) — Agents can access raw API keys; request for masked secrets system
- [#49876](https://github.com/openclaw/openclaw/issues/49876) — Hallucinated output on tool failure (trust & safety issue)

### New bugs today:
- **#100460** → Fixed by [#100482](https://github.com/openclaw/openclaw/pull/100482) (Ollama stream ending early breaks fallback chain)
- **#99367** → Fixed by [#100542](https://github.com/openclaw/openclaw/pull/100542) (heredoc quoting misinterpreted as command stages)
- **#100254** → Fixed by [#100539](https://github.com/openclaw/openclaw/pull/100539) (claude-sonnet-5 missing from adaptive thinking allowlists)
- **#98978** → Fixed by [#100544](https://github.com/openclaw/openclaw/pull/100544) (root `--help` descriptions out of sync)

---

## 6. Feature Requests & Roadmap Signals

### Likely in next release:
- **OpenAI GPT-5.6 support** — **already shipped** in v2026.7.1-beta.2
- **Channel pairing request hook** ([PR #97733](https://github.com/openclaw/openclaw/pull/97733)) — plugin hook for new pairing requests; size XL, P2, needs proof
- **Keep active session goals in context** ([PR #100468](https://github.com/openclaw/openclaw/pull/100468)) — L-sized PR with QA scenarios, waiting on author
- **UI: GitHub issue/PR hover previews** ([PR #100434](https://github.com/openclaw/openclaw/pull/100434)) — XL PR, sufficient proof, waiting on author
- **iOS richer Settings About screen** ([PR #100531](https://github.com/openclaw/openclaw/pull/100531)) — M-sized, sufficient proof, waiting on author

### Strongly requested (backlog):

| Feature | Issue | Comments | Predict |
|---------|-------|----------|---------|
| Linux/Windows desktop apps | [#75](https://github.com/openclaw/openclaw/issues/75) | 110 | Not imminent — help wanted |
| Masked secrets system | [#10659](https://github.com/openclaw/openclaw/issues/10659) | 13 | P1, security impact — could be next |
| Filesystem sandboxing config | [#7722](https://github.com/openclaw/openclaw/issues/7722) | 9 | P2, security review needed |
| Skill priority configuration | [#50199](https://github.com/openclaw/openclaw/issues/50199) | 8 | P2, ux-friction |
| Session snapshots (save/load) | [#13700](https://github.com/openclaw/openclaw/issues/13700) | 6 | P2, off-meta |
| Multi-index embedding memory | [#63990](https://github.com/openclaw/openclaw/issues/63990) | 6 | P2, waiting on product decision |

---

## 7. User Feedback Summary

### Pain points expressed:

1. **Platform gaps**: "We have apps for macOS, iOS and Android... Linux and Windows are missing" (#75) — 81 upvotes
2. **Build friction**: Users want prebuilt Android APKs, not source compilation (#9443)
3. **Reliability anxiety**: Session state corruption, memory leaks (14.7GB after 4 days), subagent persistence causing unresponsive main sessions (#54155, #47975)
4. **Model compatibility whack-a-mole**: Cron agentTurn sends wrong thinking values to GPT-5-nano (#63918); claude-sonnet-5 missing from allowlists (#100254)
5. **Missing features with workaround burden**: Users manually scripting auto-update workflows (#12855), deny-list for exec approvals (#6615), dedicated channel for lifecycle warnings (#45565)
6. **Language barrier**: Chinese user reporting hardcoded working path from a developer named wangtao (#51429) — this was fixed but the incident eroded trust

### Satisfaction signals:
- **High engagement**: 349 PRs merged/closed today indicates active development
- **1 new release** with GPT-5.6 support — shows responsiveness to latest models
- **Contribution welcome**: "help wanted" label on many issues; community members creating PRs (e.g., #100482, #100542)

---

## 8. Backlog Watch

### Critical issues with no recent maintainer activity:

| Issue | Created | Days Open | Severity | Notes |
|-------|---------|-----------|----------|-------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | 187 | P2 | Most upvoted issue (81👍), no fix PR |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | 2026-02-28 | 129 | P1 | Bootstrap files ignored; has linked PR but open |
| [#54155](https://github.com/openclaw/openclaw/issues/54155) | 2026-03-25 | 104 | P1 | Memory leak 389MB→14.7GB; no fix PR |
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | 2026-03-13 | 116 | P1 | Cron jobs silently time out; no fix PR |
| [#49876](https://github.com/openclaw/openclaw/issues/49876) | 2026-03-18 | 111 | P1 | Hallucinated cron output; no fix PR, needs security review |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) | 2026-03-14 | 115 | P2 | gh-issues skill untrusted injection; needs security review |

### Stale but important PRs waiting for maintainer:

| PR | Title | Status | Wait time |
|----|-------|--------|-----------|
| [#94130](https://github.com/openclaw/openclaw/pull/94130) | Handle Anthropic max_turns stop reason | Ready for maintainer look | 19 days |
| [#96134](https://github.com/openclaw/openclaw/pull/96134) | Remote SSH gateway rejects plaintext before tunnel connects | Ready for maintainer look | 13 days |
| [#99700](https://github.com/openclaw/openclaw/pull/99700) | Policy: repair required deny tool findings | Ready for maintainer look | 3 days |
| [#96073](https://github.com/openclaw/openclaw/pull/96073) | OpenShell non-secret env config | Ready for maintainer look | 13 days |

**Notable:** The project has **no stale bot auto-closure** in evidence — issues from Jan/Feb 2026 remain open with "clawsweeper:no-new-fix-pr" and "needs-maintainer-review" labels. This suggests maintainer review is the bottleneck for many longstanding issues.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the community digest summaries for 2026-07-06.

---

## Cross-Project Ecosystem Comparison Report — 2026-07-06

### 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is undergoing a period of intense, concurrent development across multiple specialized projects. The landscape is defined by a core reference implementation (OpenClaw) that sets the standard for breadth and community scale, alongside a tier of highly active, differentiated forks (Hermes Agent, IronClaw, ZeroClaw, NanoBot) competing on specific architectural features like agent specialization, modularity, and security hardening. A second tier of projects (PicoClaw, NanoClaw, CoPaw, LobsterAI) are engaged in focused maintenance and niche feature development, while several others (NullClaw, TinyClaw, Moltis) show no recent activity, indicating consolidation or dormancy. The dominant technical themes across the active ecosystem are agent stability (loop control, state management), security hardening (secret masking, SSRF prevention, sandboxing), and the drive toward cross-provider model flexibility.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release (24h) | Health Score (Qualitative) |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | Yes (v2026.7.1-beta.2) | Strong, but backlog-strained |
| **Hermes Agent** | 50 | 50 | No | Active, backlog-heavy |
| **NanoBot** | 1 | 18 | No | Moderate-High, feature-heavy |
| **IronClaw** | 4 | 28 | No | Robust, high velocity |
| **ZeroClaw** | 23 | 50 | No | High, fast iteration |
| **CoPaw** | 12 | 5 | No | Moderate, sprint mode |
| **NanoClaw** | 0 | 6 | No | Steady, consolidation |
| **PicoClaw** | 0 | 7 | No | Moderate, maintenance |
| **LobsterAI** | 0 | 2 | No | Stable, low churn |
| **NullClaw** | 0 | 0 | No | Inactive |
| **TinyClaw** | 0 | 0 | No | Inactive |
| **Moltis** | 0 | 0 | No | Inactive |
| **ZeptoClaw** | 0 | 0 | No | Inactive |

### 3. OpenClaw's Position

OpenClaw remains the ecosystem's **undisputed core reference**, with a community and activity volume that is an order of magnitude larger than any peer (500+ issues/PRs updated daily vs. 50 for the next closest, Hermes Agent). Its advantages include a **mature release pipeline** (new beta with GPT-5.6 support), the most **extensive platform support** (macOS, iOS, Android, with CLI), and a vast contributor base. However, it suffers from a **significant maintainer bottleneck**; critical P0/P1 issues (e.g., Android APK releases, memory leaks, security concerns) have been open for months, directly contrasting with the more focused, faster-moving forks.

**Key technical differences:** OpenClaw is a **monolithic reference implementation** aiming for maximal feature breadth. Peers are emerging as **optimized, modular derivatives**: IronClaw is pursuing a "Reborn" plug-in architecture, ZeroClaw is splitting its core vs. integrations, and NanoBot is aggressively building a subagent/standalone agent ecosystem. OpenClaw's community is *consumer-heavy* (demanding desktop parity, prebuilt binaries, and consumer subscription integration), whereas its peers see more *developer/enterprise* engagement (security RFCs, MCP stability, deployment infrastructure).

### 4. Shared Technical Focus Areas

The following requirements are emerging independently across multiple major projects, pointing to ecosystem-wide pain points and investment areas:

- **Agent Loop Stability & Cost Control:**
    - *Projects:* OpenClaw, IronClaw, ZeroClaw, NanoBot, CoPaw
    - *Specific Needs:* Preventing infinite tool-call loops (IronClaw #5666), handling "hallucinated" output on tool failure (OpenClaw #49876), fixing silent context truncation (Hermes #43900, IronClaw #5663), and preventing duplicate skill directories (NanoBot #4554).

- **Security Hardening (Secrets & Injection):**
    - *Projects:* OpenClaw, IronClaw, NanoBot, ZeroClaw
    - *Specific Needs:* Masked secrets/raw API key protection (OpenClaw #10659), SSRF prevention via pinned DNS (NanoBot #4671), untrusted content injection prevention (OpenClaw #45740), and fixing bridged tool disclosure (IronClaw #5647).

- **Cross-Provider Model & API Compatibility:**
    - *Projects:* OpenClaw, ZeroClaw, CoPaw, NanoBot
    - *Specific Needs:* OpenAI GPT-5.6 and OAuth support (OpenClaw), OpenAI API adapter for broader tooling (ZeroClaw #8603), model ID matching across providers (CoPaw #5784), and long tool name constraints from MCP servers (NanoBot #4700).

- **Multi-Platform & Mobile Reliability:**
    - *Projects:* OpenClaw, ZeroClaw, CoPaw, LobsterAI
    - *Specific Needs:* Android APK availability (OpenClaw), Termux install fixes (ZeroClaw), Feishu bot response degradation (CoPaw), and mobile WebUI content truncation (CoPaw #5787).

### 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | ZeroClaw | NanoBot | Hermes Agent | CoPaw |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary Target User** | Broad consumer / power user | Developer / Enterprise ops | Developer / Engineer | Developer / Specialist | Power user / Community | Enterprise / Team |
| **Architecture Focus** | Monolithic reference | Modular "Reborn" plug-in | SOP/Goal-mode control plane | Subagent / MCP orchestration | Multi-platform UI integration | Agent memory & scheduling |
| **Key Strength** | Largest community, widest platform support | Fastest iteration, strong security response | Goal-driven SOP, heavy bug-fix sprint | Feature velocity (MCP, STT, subagents) | Strong UX (Desktop, WebUI, CLI) | Active community bug reporting |
| **Key Bottleneck** | Maintainer bandwidth | Open dependency bumps | Emerging UX/Security bugs | Low community discussion | Stale PR backlog | Maintainer merge velocity |

### 6. Community Momentum & Maturity

- **Tier 1 (Highest Velocity, Rapid Iteration):** **IronClaw** (28 PRs, aggressive "Reborn" refactor) and **ZeroClaw** (50 PRs, closing SOP/Goal mode milestone) are the fastest-moving projects, dominated by core teams shipping large architectural changes.
- **Tier 2 (High Activity, Feature-Heavy):** **Hermes Agent** (50 PRs, large bug-fix and security sprint) and **NanoBot** (18 PRs, strong subagent and STT feature pipeline) are actively expanding capabilities.
- **Tier 3 (Steady / Consolidating):** **OpenClaw** (massive scale but high friction), **NanoClaw** and **PicoClaw** are in maintenance and focused feature delivery cycles, not major architectural pivots.
- **Tier 4 (Low / Inactive):** **LobsterAI**, **NullClaw**, **TinyClaw**, **Moltis**, **ZeptoClaw** show negligible or no development momentum in the last 24 hours.

### 7. Trend Signals

- **The "Agentic Loop" Reliability Crisis:** The repeated, project-independent focus on preventing infinite tool loops, hanging turns (`browser_open` in ZeroClaw), and hallucinated outputs signals a **core UX bottleneck** for agent adoption. Solving this deterministically (IronClaw's "corrective nudge," NanoBot's MCP reconnect fixes) is a critical value proposition.

- **Consumer Subscription Model Clash:** The top community demand across the ecosystem is for **consumer OAuth integration** (Hermes #25267, OpenClaw GitHub integrations). Users are demanding to bring their existing subscriptions (Claude, etc.), resisting an "API key only" model.

- **Security as a Feature, Not an Afterthought:** The volume of in-flight security fixes (SSRF, secret masking, allowlist stripping, injection prevention) across IronClaw, NanoBot, and ZeroClaw indicates that **security hardening is now a key competitive differentiator**, especially for enterprise-targeted forks.

- **MCP as the Universal Interface Layer:** MCP reliability (connectivity, crash handling, name constraints) is a **shared, emerging pain point** across NanoBot, ZeroClaw, and Hermes, suggesting that MCP is becoming the standard tool integration protocol, and its stability is a prerequisite for production readiness.

- **The "Model Agnosticism" Premium:** The demand for custom API base URLs (NanoBot #4702), per-model tool-call handling (IronClaw #5665), and OpenAI API adapters (ZeroClaw #8603) highlights that projects that can abstract away the volatility of individual LLM providers will win trust from cost-conscious and local-first user segments.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-06

## 1. Today's Overview

NanoBot shows **moderate to high activity**, with **1 new open issue** and **18 pull requests updated** in the last 24 hours, of which **3 were merged or closed**. The project is in a **feature-heavy development phase**, particularly around **subagent capabilities, MCP reliability, and security hardening**. No new releases were published today. Three closed PRs indicate steady progress on stability improvements, especially in the **MCP reconnect path** and **OAuth provider support**.

---

## 2. Releases

**No new releases today.**

---

## 3. Project Progress — Merged/Closed PRs

Three PRs were merged or closed in the last 24 hours:

| PR | Title | Status | Summary |
|----|-------|--------|---------|
| [#4554](https://github.com/HKUDS/nanobot/pull/4554) | fix(memory): block Dream from creating duplicate skills via write guard | **CLOSED** | Prevents Dream from creating duplicate skill directories. Returns an error to edit existing skills instead. |
| [#4441](https://github.com/HKUDS/nanobot/pull/4441) | fix(mcp): force-close streamable_http generator on reconnect failure | **CLOSED** | Fixes gateway crash (`RuntimeError: Attempted to exit cancel scope in a different task`) during MCP server session termination. |
| [#4699](https://github.com/HKUDS/nanobot/pull/4699) | fix(providers): add Anthropic OAuth with env-var-aware login/logout | **CLOSED** | Adds Anthropic OAuth integration, reading `CLAUDE_CODE_OAUTH_TOKEN` environment variable alongside file-based storage, addressing dual-source UX issues. |

**Key takeaway:** The project resolved a critical MCP crash bug and improved OAuth handling, while fixing a memory/skills management issue.

---

## 4. Community Hot Topics

Most active discussions and PRs (low comment volume overall — most PRs have 0 comments):

| Item | Type | Comments/Reactions | Summary |
|------|------|--------------------|---------|
| [#4702](https://github.com/HKUDS/nanobot/issues/4702) | Issue (Open) | 0 comments, 0 reactions | **Feature request:** Support custom API Base URL and request headers for Telegram Channel. User wants to use **custom Telegram Bot API servers** (e.g., via third-party or self-hosted endpoints) instead of hardcoded `api.telegram.org`. |
| [#4353](https://github.com/HKUDS/nanobot/pull/4353) | PR (Open) | 0 comments | **STT reliability:** Converts `.ogg`/`.opus`/`.m4a` audio to WAV 16k mono via ffmpeg before STT, fixing intermittent empty returns from AssemblyAI. |
| [#4697](https://github.com/HKUDS/nanobot/pull/4697) | PR (Open) | 0 comments | **Subagent MCP inheritance:** Adds configurable MCP server inheritance for specialist subagents, enabling database/search access without raw shell calls. |
| [#4623](https://github.com/HKUDS/nanobot/pull/4623) + [#4624](https://github.com/HKUDS/nanobot/pull/4624) | PRs (Open) | 0 comments | **Subagent enhancements:** Add subagent model override and aggregated result mode — two complementary features for subagent orchestration. |

**Underlying needs:** The community is pushing for **platform extensibility** (custom Telegram API endpoints), **subagent autonomy** (model override, MCP inheritance), and **cross-platform STT reliability**. These indicate growing deployments in **non-standard network environments** and complex multi-agent workflows.

---

## 5. Bugs & Stability

### Critical / P0
- **None reported today.**

### High Severity (P1)
| Issue | Summary | Fix PR |
|-------|---------|--------|
| [#4764](https://github.com/HKUDS/nanobot/pull/4764) | **MCP gateway crash** on server idle timeout: reconnect path closes old transport and opens new one, with risk of cancel scope task mismatch. | Open PR [#4764](https://github.com/HKUDS/nanobot/pull/4764) (author notes it's "not elegant but working") |
| [#4701](https://github.com/HKUDS/nanobot/pull/4701) | **Agent loop crash** from unhandled MCP SDK exceptions in `execute` methods for tool, resource, and prompt. | Open PR [#4701](https://github.com/HKUDS/nanobot/pull/4701) — catches `BaseException` |
| [#4700](https://github.com/HKUDS/nanobot/pull/4700) | **API errors from long tool names:** MCP-derived names exceeding model API name length constraint cause `Invalid ... names' must be strings ...` errors. | Open PR [#4700](https://github.com/HKUDS/nanobot/pull/4700) |
| [#4545](https://github.com/HKUDS/nanobot/pull/4545) | **Windows command execution** inconsistency: single-line commands via `cmd.exe` vs multi-line via PowerShell — cross-drive `cd` fails. | Open PR [#4545](https://github.com/HKUDS/nanobot/pull/4545) |
| [#4671](https://github.com/HKUDS/nanobot/pull/4671) | **SSRF vulnerability:** Unvalidated DNS resolution in web_fetch and MCP HTTP probes — potential SSRF bypass. | Open PR [#4671](https://github.com/HKUDS/nanobot/pull/4671) — pins DNS to validated IPs |

### Medium Severity (P2)
| Issue | Summary | Fix PR |
|-------|---------|--------|
| [#4698](https://github.com/HKUDS/nanobot/pull/4698) | **Inconsistent OAuth CLI error messages** across CLI and WebUI for `oauth-cli-kit` import failures. | Open PR [#4698](https://github.com/HKUDS/nanobot/pull/4698) |

**Assessment:** Four P1 bugs with open fix PRs — MCP stability is the primary concern, with SSRF security and Windows compatibility also receiving attention. The P1 fix for `#4545` (Windows commands) has been open since June 26 without merge.

---

## 6. Feature Requests & Roadmap Signals

### From Today's Issue
| Issue | Feature | Likelihood for Next Release |
|-------|---------|---------------------------|
| [#4702](https://github.com/HKUDS/nanobot/issues/4702) | Custom API Base URL and request headers for Telegram Channel | **Medium** — still just an enhancement request with no PR; depends on community demand and proxy configuration complexity |

### From Active PRs (Strong Roadmap Signals)
| PR | Feature | Analysis |
|----|---------|----------|
| [#4697](https://github.com/HKUDS/nanobot/pull/4697) | Configurable MCP inheritance for subagents | **High — likely next version.** Author is a frequent contributor (franciscomaestre), and this addresses a major gap in subagent capabilities. |
| [#4623](https://github.com/HKUDS/nanobot/pull/4623) | Spawn model override for subagents | **High** — complements MCP inheritance, enables specialized subagent models. |
| [#4624](https://github.com/HKUDS/nanobot/pull/4624) | Aggregated subagent result mode | **High** — improves subagent output management, avoids flooding the main agent with real-time results. |
| [#4625](https://github.com/HKUDS/nanobot/pull/4625) | Extra bwrap bind roots for exec sandbox | **Medium** — specific to Linux sandbox deployments, useful for exposing user tool directories. |
| [#4620](https://github.com/HKUDS/nanobot/pull/4620) | CLI heartbeat trigger command | **Medium** — addresses long-standing request (#3437) for manual heartbeat triggering via CLI. |
| [#4686](https://github.com/HKUDS/nanobot/pull/4686) | Canonical OpenCode provider support | **Medium** — standardizes provider naming, likely a cleanup/foundation feature. |

**Prediction:** The **subagent ecosystem improvements** (#4697, #4623, #4624) are the strongest candidates for the next release, as all three are from different frequent contributors and address clear user needs. The **heartbeat trigger** (#4620) may also ship as it resolves a GitHub issue from 2024.

---

## 7. User Feedback Summary

### Pain Points Expressed
- **Telegram API inflexibility** (#4702): User in complex network environments cannot use custom API endpoints beyond proxy support.
- **Windows command inconsistency** (#4545, fixing #4544): Cross-drive `cd` failures and POSIX-style `$VAR`/`$(...)` staying literal under `cmd.exe` frustrate Windows users.
- **STT failures with WhatsApp audio** (#4353): AssemblyAI returning empty strings for `.ogg`/`.opus` files — affects real-time voice interactions.
- **MCP session crashes** (#4764, #4441): Production reliability issue — gateway crashes when MCP servers idle timeout.
- **Long tool name errors** (#4700): MCP servers with descriptive names break model API constraints.

### Positive Signals
- **Subagent flexibility** is being actively developed, indicating growing sophistication of multi-agent use cases.
- **Security hardening** (SSRF pinning in #4671) shows responsible maintenance practices.
- **OAuth UX improvements** (#4699, #4698) suggest real-world OAuth adoption.

### Use Cases Implied
- Multi-platform deployments (Telegram + Feishu + WhatsApp)
- Custom enterprise networks requiring custom API endpoints
- Multi-agent orchestration with specialized subagents (database, search)
- Voice-first interactions via WhatsApp
- Self-hosted, secure deployments concerned with SSRF

---

## 8. Backlog Watch

### Important Issues/PRs with Extended Dwell Time

| Item | Age | Status | Concern |
|------|-----|--------|---------|
| [#4353](https://github.com/HKUDS/nanobot/pull/4353) — STT audio conversion | **21 days** (since June 15) | Open PR | No maintainer activity in 2+ weeks; affects real-world WhatsApp transcription reliability |
| [#4406](https://github.com/HKUDS/nanobot/pull/4406) — Serper.dev web search provider | **18 days** (since June 18) | Open PR | Awaiting maintainer review; adds Google search via Serper API — a minor but useful feature |
| [#4545](https://github.com/HKUDS/nanobot/pull/4545) — Windows command fix | **10 days** (since June 26) | Open PR | P1 bug fix for Windows users; closing issue #4544 directly |
| [#4441](https://github.com/HKUDS/nanobot/pull/4441) — MCP reconnect crash fix | **Closed today** | ✅ Resolved | This was a significant backlog item finally merged |

**Maintainer attention needed:**
1. **PR #4353** (STT audio conversion) — longest open without merge, blocks WhatsApp voice note reliability
2. **PR #4545** (Windows commands) — P1 bug fix for Windows users, needs review and merge
3. **Issue #4702** (Telegram API flexibility) — new but could signal a pattern of custom networking needs

---

## Overall Project Health

| Dimension | Assessment |
|-----------|------------|
| **Activity** | ✅ High — 18 PRs updated, 3 merged/closed |
| **Stability** | ⚠️ Moderate — 4 P1 bugs open with fix PRs, MCP crash risks |
| **Feature Velocity** | ✅ High — subagent system, heartbeat, STT, OAuth all making progress |
| **Community Engagement** | 🟡 Low (few comments/reactions on issues) |
| **Security** | ✅ Improving — SSRF hardening in progress |
| **Windows Support** | 🟡 Needs attention — P1 bug open for 10 days |

**Bottom line:** NanoBot is actively evolving with significant feature work, but MCP stability and Windows compatibility are the two areas needing most immediate maintainer focus. The subagent improvements signal an important architectural pivot toward agent specialization.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — July 6, 2026

## Today's Overview
The Hermes Agent project maintained a high level of activity, with 50 issues and 50 pull requests updated in the last 24 hours. The project is in a strong iteration phase, driven by a combination of active bug fixing (8 merged/closed PRs), community feature requests, and security hardening work. While no new releases dropped today, the volume of open issues (45 active) and PRs (42 open) suggests a healthy but backlog-heavy development cycle. Notably, several security-and-stability sweeper PRs landed, addressing message delivery risks and webhook body limits across multiple platforms. The community is actively engaged, with top-voted feature requests—particularly around Claude subscription integration (41 👍)—indicating clear user demand for flexible provider models.

## Releases
No new releases were published today. The project remains in a release gap, with significant unmerged work accumulating across security, platform integration, and CLI UX features.

## Project Progress
**Merged/Closed PRs (8 today):**

- **[#59284]** `fix(kanban): goal-gate judge unpack matches judge_goal's 4-tuple` — Fixes a fail-open-by-crash bug in the goal-mode completion gate
- **[#59169]** `fix(photon): reinstall sidecar npm deps after version bump` — Resolved an update failure where `hermes update` didn't refresh Photon sidecar dependencies
- **[#54935]** `fix(feishu): buffer oversized chunked bodies before 413` — Security fix for Feishu webhook body limits
- **[#54940]** `fix(whatsapp): buffer oversized bodies before 413` — Parallel fix for WhatsApp Cloud webhook
- **[#59257]** `fix(cli): session title lost on exit` — Addressed regression from desktop-first commits affecting CLI/TUI exit summary
- **[#9318]** `fix(agent): auxiliary client api_key fallback` — Fixed empty api_key falling through to "no-key-required" placeholder

**Notable open PRs with recent activity:**
- **[#59295]** `[OPEN] feat(session-search): scope default discovery to current shared chat` — Improves multi-chat gateway UX
- **[#59292]** `[OPEN] fix(cli+bluebubbles+agent+kanban): 4 bugs` — Bundled fixes for IndexError, OOM, SOUL.md fallback, kanban delivery loop
- **[#59275]** `[OPEN] feat: auto-detect OS appearance changes mid-session` — Adds live skin switching for light/dark mode

## Community Hot Topics

### Most Active Issues by Comments
1. **[#25267 — Claude Agent SDK model provider with subscription OAuth](https://github.com/NousResearch/hermes-agent/issues/25267)** — 9 comments, 41 👍
   *Underlying need:* Users on Claude subscriptions want to use Hermes without paying double (subscription + API tokens). This is the highest-reacted issue and reflects a strong community desire for consumer-friendly provider integration.
2. **[#34390 — Dashboard --allowed-hosts flag for reverse-proxy access](https://github.com/NousResearch/hermes-agent/issues/34390)** — 9 comments
   *Underlying need:* Users deploying behind Tailscale or reverse proxies are blocked by DNS rebinding protection. They want secure-by-default but configurable host header validation.
3. **[#43900 — Ollama context window capped at 4096 tokens](https://github.com/NousResearch/hermes-agent/issues/43900)** — 8 comments
   *Underlying need:* Local model users are hitting silent context truncation, causing garbled responses and wasted tokens. Hermes reads but does not actually apply the larger `num_ctx` from GGUF metadata.

### Most Discussed PRs
- **[#59292]** `fix: 4 bugs in cli+bluebubbles+agent+kanban` — Community bug hunt consolidation
- **[#59278]** `fix: isolate per-subscription failures in kanban notifier` — Preventing global delivery deadlock

## Bugs & Stability

### Critical Severity (P2)
- **[#59224]** `[P2] Classic CLI /resume hides Desktop sessions` — Sessions created in Desktop are invisible to CLI `/resume`. **Fix PR #59281 exists.**
- **[#57129]** `[P2] MCP client permanently abandons server after 5 failed reconnects` — Transient upstream failure permanently kills MCP tools. No fix PR yet.
- **[#59280]** `[P2] BlueBubbles webhook OOM` — Missing `client_max_size` risk. **Fix PR #59280 exists.**
- **[#59236]** `[P2] Cron marker leaking into interactive gateway approvals` — Security boundary risk. **Fix PR in review.**

### Medium Severity (P3)
- **[#41566]** `[P3] Desktop shows connection error despite verified HTTPS/WSS` — UX regression making desktop app appear broken.
- **[#38669]** `[P3] Web UI chat scrollbar cannot scroll to bottom` — Reproducible browser-side scroll lock.
- **[#59272]** `[P2] QQAdapter.connect() missing is_reconnect parameter` — TypeError on every reconnect attempt.
- **[#59169]** `[P3] Photon sidecar deps not reinstalled on update` — Fixed today.

### Security-Related (Sweeper Labels)
- **[#59235]** `[P3] Plain-formatter redaction gaps for split secrets and tracebacks` — Secrets may leak in logs after %-formatting assembly.
- **[#54935/54940]** `[P3] Webhook body buffer before 413 check` — Fixed for Feishu and WhatsApp; pattern may apply to other platforms.

## Feature Requests & Roadmap Signals

### High-Vote Features Likely for Next Version
1. **Claude subscription OAuth provider** (#25267, 41 👍) — Strongest demand signal. Would allow Claude subscribers to use Hermes without separate API billing.
2. **Generalized event substrate for Kanban notifications** (#49190, 4 comments) — Would transform Kanban from hardwired platform-specific notifications to a pluggable event system with delivery adapters.
3. **Automated workspace memory** (#38552, 3 comments) — Agent remembering what directories are for across sessions. Complementary to ongoing memory work in #33856.

### Emerging Features in PR Pipeline
- **Custom HTTP headers for provider requests** (#14314, open since April) — Still active after 2+ months, indicates deliberate review.
- **Torben backend productionization** (#52780) — Signal-facing operator for backend capabilities.
- **OS appearance auto-detection for skin switching** (#59275) — Quality-of-life UX improvement.
- **Bulk archive for desktop sessions** (#39376) — Addresses desktop sidebar clutter at scale.

### Features with Implementation Activity
- **Default YOLO mode for desktop** (#39375) — Multiple PRs over months suggest near-completion.
- **Approval layer improvements** (#43157, #36920, #59235) — Active security hardening sprint.

## User Feedback Summary

### Pain Points
- **Double billing:** "Claude-subscribed users effectively pay twice" (#25267) — Top pain point.
- **Silent failures:** Ollama users hit unannounced context caps (#43900), MCP server abandonment (#57129), Desktop connection false negatives (#41566).
- **Discoverability:** Sessions created in one UI (Desktop/WebUI) are invisible from CLI `/resume` (#59224).
- **Configuration friction:** No API key field for custom endpoints in Desktop setup (#38348); `hermes config set` bypasses system write protection (#59293).
- **Platform gaps:** QQ Bot silently drops media attachments (#37315); WhatsApp bridge shows console window on Windows (#59285).

### Use Cases
1. **Consumer AI assistant:** Users want to bring their Claude subscription (OAuth, not API key).
2. **Local-first power users:** Running Ollama/vLLM with large context models.
3. **Multi-platform teams:** Deploying behind Tailscale/reverse proxies; using Desktop alongside CLI/WebUI.
4. **Security-conscious admins:** Seeking approval guards, publish guards, and log redaction.

### Satisfaction Signals
- Active community PRs addressing bugs (4-bug consolidation PR #59292, multiple platform webhook fixes).
- High engagement on sweeper-labeled security fixes indicates trust in the project's security response.
- Continued use of Hermes for production workflows (Torben, kanban, delegate tasks).

## Backlog Watch

### Stale Issues Needing Maintainer Attention
1. **[#5388](https://github.com/NousResearch/hermes-agent/issues/5388)** `[P2, needs-repro]` — "Context broken" (Chinese-language report from April 6). Open for 3 months with 2 comments. No reproduction steps provided. Needs triage or closure.
2. **[#14314](https://github.com/NousResearch/hermes-agent/pull/14314)** `[P3] feat: add custom header support` — Open PR since April 23 (75 days). No merge blocker identified. High-value feature for custom provider integrations.
3. **[#29914](https://github.com/NousResearch/hermes-agent/issues/29914)** `[P3] Add per-turn and per-tool-call model overrides` — Open since May 21. Describes a clear UX gap that would simplify model switching. No assignee, no PR.

### Stale PRs
- **[#14314](https://github.com/NousResearch/hermes-agent/pull/14314)** — Custom headers (75 days, no recent review commit).
- **[#36920](https://github.com/NousResearch/hermes-agent/pull/36920)** — GitHub PR publish guard (35 days, actively updated but not merged).
- **[#39375](https://github.com/NousResearch/hermes-agent/pull/39375)** — Default YOLO mode (32 days, multiple commits, no merge).

---

*Project health: Active and responsive to security issues, with strong community engagement. The backlog of open PRs (42) and active issues (45) suggests the project could benefit from a focused cleanup sprint or a point release to ship the accumulated fixes and features.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-06

*Generated from GitHub activity (sipeed/picoclaw) — Data range: 2025-07-05 to 2025-07-06*

---

## 1. Today's Overview

Project activity is moderate with 7 items updated in the last 24 hours and one fresh code submission. A high-priority feature request to replace the insecure `libolm` with `vodozemac` (Issue #3088) remains open with active community discussion. The stale-bot initiated closure of a Chinese-language bug report (#3150) citing a "memory loss" symptom, but a corresponding fix PR (#3226) was opened the same day, suggesting maintainers are addressing the root cause. No new releases were published; the project is in a maintenance-and-refactoring phase.

---

## 2. Releases

No new releases in the reporting period.

---

## 3. Project Progress (Merged/Closed PRs)

**1 PR was merged/closed today:**
- **[#3189]** [CLOSED] `fix(line): explicitly ignore resp.Body.Close() errors` — Author: chengzhichao-xydt
  - **What:** Suppresses non-critical close errors in the LINE channel `Send` method and `classifySDKError` helper (both already had nil checks).
  - **Significance:** Low-impact cleanup — improves code hygiene but no functional change.

---

## 4. Community Hot Topics

### Most Active Issue
- **[#3088]** [OPEN — high priority, help wanted] **Use vodozemac instead of libolm**
  - Author: pbsds | Created: 2026-06-09 | Comments: **6** | 👍: **2**
  - URL: [sipeed/picoclaw Issue #3088](https://github.com/sipeed/picoclaw/issues/3088)
  - **Analysis:** This is the most-reacted-to open issue. The community is pushing to replace `libolm` (unmaintained, insecure) with `vodozemac` (official Matrix replacement). The request asks to make `libolm` optional at compile time. Given its "high priority" label and 2 upvotes, this is the top community demand.

### Most Active Pull Request (Discussion)
- **[#3226]** Open (just submitted) — `fix(tools): stop write_file from coaching destructive overwrite (#3150)`
  - Author: ACMYuechen | Created: 2026-07-05 | Comments: 0 yet
  - URL: [sipeed/picoclaw PR #3226](https://github.com/sipeed/picoclaw/pull/3226)
  - **Analysis:** Fresh fix directly addressing the "memory loss" bug. The PR description explains the agent was coached by `write_file`'s guard message to overwrite memory files — a subtle safety gap. Likely to become today's most discussed item.

---

## 5. Bugs & Stability

| Issue | Severity | Status | Notes |
|-------|----------|--------|-------|
| [#3150] "它给自己整失忆了" (self-induced memory loss) | **High** | CLOSED (stale) + fix PR exists | Bug caused agent to overwrite `memory/MEMORY.md` due to `write_file`'s destructive overwrite coaching. Root cause confirmed by PR #3226. |
| [#3189] LINE channel `resp.Body.Close()` error handling | **Low** | Fixed & merged | No runtime impact; noise suppression only. |

**Key finding:** The #3150 bug is not trivial — it represents an agent-safety regression where the tooling itself pushed the model toward destructive behavior. Fix PR #3226 is critical and should be reviewed promptly.

---

## 6. Feature Requests & Roadmap Signals

### Strongest Signal
- **[#3088] — vodozemac migration** (high priority, help wanted)
  - **Prediction for v0.2+:** Likely targeted for next minor release. `libolm` deprecation is a security mandate; the official Matrix replacement (`vodozemac`) is mature. The "make libolm optional at compile time" phrasing suggests a phased rollout rather than immediate hard replacement.

### Weaker Signals
- **Dependency bumps:** PR #3192 (bumps GoReleaser Dockerfiles from alpine:3.21→3.23) signals ongoing maintenance, not feature work.
- **DeltaChat refactoring:** PR #3222 (-320 LOC) shows refactoring effort but likely already in review, not a new request.

---

## 7. User Feedback Summary

| Pain Point | Evidence | Sentiment |
|------------|----------|-----------|
| **Memory corruption / agent over-write** | #3150 bug — the agent overwrote its own memory because `write_file` coached it toward replacement | Negative — tool UX flaw that destroys user data |
| **Dependency security** | #3088 request to drop `libolm` | Concern — users want modern, secure crypto |
| **Code duplication / config clutter** | PR #3191 (duplicate `.gitignore` entry) | Minor irritation — signals project maturity / need for cleanup |

**Notable:** The silence around #3150's closure as "stale" before a fix PR appeared suggests the stale-bot may have acted too aggressively. User @svier0 (the reporter) may feel unheard.

---

## 8. Backlog Watch

### Unanswered Issues Needing Maintainer Attention
- **[#3088]** (vodozemac migration) — Created **27 days ago**, 6 comments, 2 upvotes, maintainers have not responded. **Severity: High.** This is the most important open issue and is neglected.

### Unanswered PRs
- **[#3192]** (Docker bump) — Created **9 days ago**, no maintainer comment. **Severity: Low** (minor bump).
- **[#3191]** (`.gitignore` dedup) — Created **9 days ago**, no maintainer comment. **Severity: Very low** (cosmetic).
- **[#3222]** (DeltaChat refactor) — Created **3 days ago**, no maintainer comment yet. **Severity: Medium** (significant code deletion; needs review).

### Alert
- **[#3150]** was closed by stale-bot despite an active fix PR (#3226) being opened the same day. Recommend reopening #3150 or marking it as a duplicate of #3226 to preserve context.

---

*Digest generated 2026-07-06 from sipeed/picoclaw GitHub data. All links point to the official repository.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-06

---

## 1. Today's Overview

NanoClaw is showing steady, focused development activity with 6 pull requests updated in the last 24 hours, though no new issues were filed or closed. The project appears to be in a **consolidation phase**, with several long-running PRs receiving critical refreshes and a balanced mix of open and merged work. Three PRs were merged/closed — including two significant feature additions (per-group guardrails and Codex persona support) that shipped over the weekend — while three remain open. No new releases were cut today, but the churn on open PRs suggests maintainers are actively reviewing and integrating contributions. Overall project health is **good**, with substantive feature work advancing across skill infrastructure, setup flows, and container management.

---

## 2. Releases

**No new releases published today.** The last release remains unspecified; however, the volume of merged PRs (particularly #2726 for guardrails and #2908 for Codex template agents) suggests a release may be forthcoming once the remaining open PRs (#2949, #2909, #2036) are resolved.

---

## 3. Project Progress

Three PRs were merged or closed in the last 24 hours, representing meaningful feature advancement:

| PR | Title | Summary |
|----|-------|---------|
| [#2726](https://github.com/nanocoai/nanoclaw/pull/2726) | feat: add /add-guardrails skill | **Merged.** Adds per-agent-group input/output guardrails with deterministic regex/keyphrase rules, `block`/`flag` actions, chat alerts, and host-side quarantine audit trail. Fails closed on broken configurations. |
| [#2766](https://github.com/nanocoai/nanoclaw/pull/2766) | feat(channels): add .format-lint-off | **Closed.** Adds channel-level `.format-lint-off` toggle, allowing per-channel suppression of formatting/linting checks. |
| [#2908](https://github.com/nanocoai/nanoclaw/pull/2908) | feat(codex): persona prepend + git-independent skill discovery | **Merged.** Enables agent-templates feature under Codex provider with persona prepend and provider-agnostic skills mirror (4 files, +122/−5). |

**Key advancement:** The Codex provider now fully supports the agent-templates system (paired with the template loader from PR #2890), and the guardrails system adds a significant security layer for production deployments.

---

## 4. Community Hot Topics

All open PRs have **zero comments and zero reactions**, indicating minimal community discussion on these items. The most notable active items by activity recency:

- **[#2949](https://github.com/nanocoai/nanoclaw/pull/2949)** — [OPEN] `feat(skill): /add-litellm — minimal model router`. Updated today (2026-07-06). This skill would add local server + optional remote provider model routing. *Author: javexed.*
- **[#2909](https://github.com/nanocoai/nanoclaw/pull/2909)** — [OPEN] `feat(setup): template setup flow in the wizard`. Updated 2026-07-05. Part 2 of the agent-templates feature, adding setup-wizard UX and first-agent stamping. *Author: amit-shafnir.*
- **[#2036](https://github.com/nanocoai/nanoclaw/pull/2036)** — [OPEN] `feat: per-group container env vars, DB-managed`. Refreshed 2026-07-04. Long-running PR (since April) converting container env vars from file-based to DB-native configuration.

The low comment/reaction count may reflect a **small core contributor set** rather than disinterest; all open PRs are authored by repeat contributors (javexed, amit-shafnir, stumpjumper).

---

## 5. Bugs & Stability

**No bug reports or stability issues were filed or updated in the last 24 hours.** No new issues exist in the dataset.

Of possible relevance:
- **PR #2036** (per-group container env vars) was refreshed on 2026-07-04 with a note that the original April revision "had gone stale/conflicting" due to DB migration 014. The refresh resolves a potential configuration regression for users relying on container environment variables.
- **PR #2726** (guardrails) notes it "fails closed on broken configurations," which is a safety-by-design pattern rather than a bug.

---

## 6. Feature Requests & Roadmap Signals

Based on active open PRs, the following features are likely approaching release:

| Feature | PR | Maturity | Next Version Likely? |
|---------|----|----------|-------------------|
| `/add-litellm` model router skill | [#2949](https://github.com/nanocoai/nanoclaw/pull/2949) | New (Jul 4) | Possible |
| Template setup wizard & first-agent stamping | [#2909](https://github.com/nanocoai/nanoclaw/pull/2909) | Part 2 of 2, waiting on template loader (#2890) | **Likely** |
| DB-managed per-group container env vars | [#2036](https://github.com/nanocoai/nanoclaw/pull/2036) | Refreshed, 3 months old | **Likely** |

**Roadmap signals:**
- **Agent templates** are clearly a major theme — PR #2908 (Codex support) and #2909 (setup wizard) together complete a significant cross-provider feature.
- **Skill ecosystem expansion** continues: `/add-litellm` (model routing) follows the pattern of `/add-guardrails` (security) as modular, installable skills.
- **Configuration modernization** is underway: moving container config from files to DB (PR #2036) aligns with earlier DB migrations.

---

## 7. User Feedback Summary

**No user comments, reactions, or feedback were captured in the last 24 hours.** The zero-comment state across all PRs and issues provides no direct signal for satisfaction or pain points.

**Indirect observations:**
- The refresh of PR #2036 after 3 months of inactivity suggests at least one user (stumpjumper) needed DB-based container environment variables badly enough to revive stale work.
- The /add-litellm skill (PR #2949) may respond to user demand for model-agnostic routing across local and cloud LLM backends.
- The guardrails feature (PR #2726, merged) likely addresses user concerns around prompt injection and credential leakage in multi-tenant or production agent deployments.

---

## 8. Backlog Watch

| Item | Age | Status | Risk |
|------|-----|--------|------|
| [#2036](https://github.com/nanocoai/nanoclaw/pull/2036) — per-group container env vars | Opened 2026-04-26 (71 days) | **Open**, refreshed 2026-07-04 | **Medium** — stale 3 months, now revived |
| [#2909](https://github.com/nanocoai/nanoclaw/pull/2909) — template setup wizard | Opened 2026-07-02 (4 days) | Open, no comments | **Low** — young, depends on merged #2890 |
| [#2949](https://github.com/nanocoai/nanoclaw/pull/2949) — /add-litellm skill | Opened 2026-07-04 (2 days) | Open, no comments | **Low** — very new |

**No issues are open**, so there is no issue backlog to flag. The PR backlog is minimal and manageable. PR #2036 is the longest-standing open item but has been actively refreshed, suggesting maintainer attention is present.

**Notable absence:** No bug reports, no issue activity, and zero community commentary. While this could indicate stability, it more likely reflects a small user base or a project where most feedback flows through other channels (Discord, private issues, etc.).

---

*Generated from NanoClaw GitHub data — snapshot: 2026-07-06 00:00 UTC*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the **IronClaw Project Digest** for **2026-07-06**.

---

## 1. Today's Overview

The IronClaw project has seen a surge of activity over the last 24 hours, with **28 pull requests** updated and **4 issues** touched, indicating high development velocity. The core team is heavily focused on three major streams: the **"Reborn" modular architecture rollout**, hardening the **Slack integration** via an OAuth migration, and improving **AI loop stability** (broken tool calls and infinite loops). While no new releases were cut today, a release PR is pending review, suggesting a major version bump is imminent. The project's overall health appears robust, though the sheer volume of open dependency bumps (some over a month old) suggests a need for a dedicated maintenance sprint.

## 2. Releases

**No new releases today.** However, PR [#5598](https://github.com/nearai/ironclaw/pull/5598) is an active release chore that proposes significant version bumps:
- `ironclaw_common`: 0.4.2 → 0.5.0 (**breaking changes**)
- `ironclaw_skills`: 0.3.0 → 0.4.0 (**breaking changes**)
- `ironclaw`: 0.24.0 → **0.29.1** (a major jump)
- `ironclaw_safety`: patch bump (compatible).
- **Migration Note:** Projects using `ironclaw_common` or `ironclaw_skills` should review their API surface for breaking changes once this release is merged.

## 3. Project Progress

**6 PRs were merged or closed today**, reflecting significant feature advancement and bug fixes:

- **Feature: Slack OAuth Migration (Stack 4/4):** PR [#5646](https://github.com/nearai/ironclaw/pull/5646) was closed, rejecting legacy `[slack]` config fields. This completes the operator-facing breaking change for the new Slack personal OAuth flow.
- **Feature: Slack OAuth Migration (Core):** PR [#5604](https://github.com/nearai/ironclaw/pull/5604) was merged, removing the old pairing flow entirely in favor of per-user OAuth.
- **Feature: Manifest-Driven Ingress:** PR [#5626](https://github.com/nearai/ironclaw/pull/5626) was merged, moving Slack route definitions from hardcoded Rust into the extension manifest.
- **Security Fix (Reborn):** PR [#5659](https://github.com/nearai/ironclaw/pull/5659) is a "PRODUCTION CHANGE" that fixes a latent security bug where bridge meta-tools (`tool_search`, `tool_describe`) could be stripped from narrowed capability allowlists.
- **Testing:** PR [#5637](https://github.com/nearai/ironclaw/pull/5637) was closed, adding a "wiring-parity tripwire" to ensure the test harness matches production composition.
- **Infrastructure:** PR [#4002](https://github.com/nearai/ironclaw/pull/4002) was closed, updating 16 GitHub Actions dependencies.

## 4. Community Hot Topics

The most active discussions revolve around **reliability of the AI agentic loop** and **security hardening**:

- **LLM Provider Tool-Call Corruption (PR #5665):** [nearai/ironclaw PR #5665](https://github.com/nearai/ironclaw/pull/5665) (by abbyshekit) addresses providers (e.g., DeepSeek, OpenRouter) leaking XML tags into tool-call arguments. This is a **high-impact** pain point for end-users.
- **Breaking Infinite Tool-Call Loops (PR #5666):** [nearai/ironclaw PR #5666](https://github.com/nearai/ironclaw/pull/5666) (by abbyshekit) introduces a "corrective nudge" to break agents stuck in identical repeated calls. This signals a deep user need for agentic loop cost-control and failure prevention.
- **Prompt Context Hardening (PR #5663):** [nearai/ironclaw PR #5663](https://github.com/nearai/ironclaw/pull/5663) (by abbyshekit) addresses silent context truncation and unbounded token costs, reflecting user frustration with unpredictable LLM bills.
- **Security Boundary Fix (PR #5659):** [nearai/ironclaw PR #5659](https://github.com/nearai/ironclaw/pull/5659) (by henrypark133) includes a regression test for the allow-strip bug, indicating tension between security and usability.

**Analysis:** The community (represented by regular contributors) is demanding better **deterministic behavior** from the AI agent, specifically when dealing with third-party model providers and complex tooling chains.

## 5. Bugs & Stability

- **Critical (Security): Issue #5647** [Bridged tool disclosure strips meta-tools](https://github.com/nearai/ironclaw/issue/5647) — A latent security bug where narrowing capability allowlists could accidentally remove the bridge's own meta-tools, breaking agent functionality. **Fix PR #5659 is ready and labeled as a "PRODUCTION CHANGE".**
- **High (Reliability): Issue #4108** [Nightly E2E Failure](https://github.com/nearai/ironclaw/issue/4108) — A Nightly E2E test run continues to fail (updated yesterday). This is a persistent stability signal that has been open for over a month. No active fix PR is linked.
- **Medium (Runtime): PR #5662** [Surface best-effort failures](https://github.com/nearai/ironclaw/pull/5662) — Addresses 90 sites where `Result` returns were silently dropped (`let _`). This is a proactive refactoring to prevent future silent failures in runtime paths.

## 6. Feature Requests & Roadmap Signals

- **Next Version Predictions:**
    - **"IronLoop" Dogfooding (PR #5580):** The addition of a dogfood config for "IronLoop" suggests the team is readying a new internal assistant tool for first-party use. Likely to ship in the next release.
    - **Optimized Turn-State Latency (PR #5667):** A draft for moving from blob-style Postgres to a `RootFilesystem-backed` store for lower latency. While still a draft, it signals a major infrastructure change in the backlog.
    - **Coverage Scope Exemptions (Issue #5657):** A tracking issue for v1-only crates being excluded from "Reborn" coverage metrics suggests the team is finalizing Reborn’s coverage standards for a stable release.
- **User-Requested Features:**
    - **Slack OAuth:** The massive Slack rework (PRs #5645, #5646) was a direct response to user pairing friction.
    - **Better Tool-Call Error Handling:** PRs #5665 and #5666 are direct reactions to agent flaky behavior, a likely top user complaint.

## 7. User Feedback Summary

While no direct user comments are visible in this data, the **code changes tell a clear story of user pain points:**
- **Frustration with LLM Inconsistency:** The focus on repairing "provider-corrupted" JSON (PR #5665) and breaking "repeated identical tool-call loops" (PR #5666) suggests users are experiencing agents that hang, waste credits, or malfunction due to upstream provider quirks.
- **Desire for Predictable Costs:** The work on "compaction truncation" and "opt-in instruction budget" (PR #5663) indicates users want to **cap token spending** and avoid mysterious bill spikes.
- **Satisfaction with Security Advances:** The quick turnaround on the bridged-tool disclosure bug (Issue #5647 → Fix PR #5659) demonstrates a maintainer commitment to agent security, which should satisfy enterprise users.

## 8. Backlog Watch

Several long-unanswered dependency bumps require attention, as they involve critical infrastructure:

- **PR #5114** [tokio-ecosystem group update](https://github.com/nearai/ironclaw/pull/5114) — Open since **June 21**. Bumps `hyper`, `tower-http`, and `tokio-tungstenite`. While low-risk, these are core networking dependencies.
- **PR #4032** [wasm group update](https://github.com/nearai/ironclaw/pull/4032) — Open since **May 25**. Bumps `wit-component` and `wit-parser` from 0.245.1 to 0.252.0. This is a major gap that could eventually cause compile issues with WebAssembly tooling.
- **Issue #4108** [Nightly E2E Failure](https://github.com/nearai/ironclaw/issue/4108) — Open since **May 27**. A persistently failing CI pipeline is a blocker for release confidence. **Needs immediate maintainer investigation.**

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-07-06**.

---

## LobsterAI Project Digest – 2026-07-06

### 1. Today's Overview
The project shows **low activity** today. No new issues were created or updated in the last 24 hours, and no new releases were cut. Activity was limited to two pull requests (PRs). The project merged **one significant feature PR** (#2273) that enhances the scheduled task UI with a redesigned card layout, status indicators, and optimistic feedback. Meanwhile, a **long-stale PR** (#1349) addressing a critical IM connectivity validation bug remains open after more than three months, still awaiting review or merge. Overall, the project appears stable but with a growing maintenance bottleneck.

### 2. Releases
**None.** No new releases were published today.

### 3. Project Progress
- **[MERGED] PR #2273 – feat(scheduledTask): task list card redesign**  
  *Author: fisherdaddy*  
  A user-facing UI enhancement that redesigns the scheduled task list cards to include status chips, a toggle switch, search functionality, and optimistic UI feedback. This improves the user experience for managing recurring tasks.  
  *Status:* Closed (Merged) on 2026-07-05.  
  *Link:* [PR #2273](https://github.com/netease-youdao/LobsterAI/pull/2273)

### 4. Community Hot Topics
- **PR #1349 – [STALE] fix(im): add real API validation for POPO connectivity test**  
  *Author: gongzhi-netease*  
  This is the **most active item** in the project, primarily because it is long-lived. The PR aims to fix a critical bug where the POPO IM connectivity test always passes regardless of invalid credentials. Despite being open since April 2, 2026, it remains unmerged. The underlying need is robust credential verification for enterprise IM integration.  
  *Activity:* 0 comments (likely direct activity on the PR itself), last updated 2026-07-05.  
  *Link:* [PR #1349](https://github.com/netease-youdao/LobsterAI/pull/1349)

### 5. Bugs & Stability
- **High Severity - POPO IM connectivity test always passes**  
  *Related PR:* #1349 (open, stale)  
  **Description:** The connectivity test for the "POPO" IM service currently returns "Verification passed" regardless of whether the `appKey` and `appSecret` are valid or even random strings. This is a **validation bypass bug** that could lead to misconfigured integrations going unnoticed.  
  **Status:** Fix PR exists, but has been stale for >3 months. No other bug reports were filed today.  
  *Link:* [PR #1349](https://github.com/netease-youdao/LobsterAI/pull/1349)

### 6. Feature Requests & Roadmap Signals
No new feature requests were explicitly filed today. However, the merged PR #2273 (task list card redesign) indicates the maintainers are prioritizing a **richer, more interactive UI** for scheduled tasks. This likely aligns with internal roadmap goals for improving the renderer area of the application.

Predictions for next version:
- **Task table UX overhaul** – Further refinements to the task list (search, filters, status chips) are likely to continue.
- **IM integration hardening** – Given the long-standing POPO bug (PR #1349), a fix for credential validation is overdue and may be forced into a hotfix release.

### 7. User Feedback Summary
**No new user feedback** was recorded today in issues or PRs. The persistent silence around PR #1349 suggests that users of the POPO IM integration are either unaware of the bug or have grown frustrated with the lack of response. The single merged PR today from an internal contributor suggests active development is happening, but the lack of community engagement (0 new issues, 0 comments) points to a **low external user contribution rate** at this time.

### 8. Backlog Watch
- **PR #1349 – fix(im): add real API validation for POPO connectivity test**  
  *Priority:* Critical | *Status:* Open & Stale (since April 2, 2026) | *Last Updated:* July 5, 2026  
  **Recommended action:** This PR has been open for **94 days**. The fix is minimal (adding a real API call instead of a simple null check). The maintainers should either review/merge this PR or close it with guidance. Leaving it stale risks confusing users and accumulating technical debt in the IM module.  
  *Link:* [PR #1349](https://github.com/netease-youdao/LobsterAI/pull/1349)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for **CoPaw**, generated from the GitHub data snapshot for **2026-07-06**.

---

## CoPaw Project Digest — 2026-07-06

### 1. Today's Overview
The CoPaw project is experiencing a **high-activity sprint** with 12 open Issues and 5 open Pull Requests updated in the last 24 hours, though **no new releases** were cut. The community is actively submitting bug reports and feature requests, with **no closed or merged PRs today**—suggesting maintainers are currently in a review/testing cycle rather than a merge phase. The project is on **version v1.1.12.post2**, and a significant portion of the backlog focuses on **cross-provider model handling, timezone inconsistencies, UI/UX bugs, and multi-user account management**. Notably, there are two **first-time contributor** PRs, indicating healthy external participation.

### 2. Releases
**None.** No new releases were published in the last 24 hours. The current stable version remains **v1.1.12.post2**.

### 3. Project Progress
**No PRs were merged or closed today.** The following five PRs remain open, indicating work in progress:

- **fix(agents): stop dropping self-paired tool messages during sanitation** (PR [#5792](agentscope-ai/QwenPaw PR #5792)) – *First-time contributor* fixes a bug where valid AgentScope 2.0 self-paired assistant messages were incorrectly dropped during message sanitation.
- **fix(console): promote formatCompact unit on rounding rollover** (PR [#5791](agentscope-ai/QwenPaw PR #5791)) – *First-time contributor* prevents non-compact strings (e.g., "1000K") from being emitted near band boundaries.
- **fix: three bug fixes (#5709, #5773, #5784)** (PR [#5786](agentscope-ai/QwenPaw PR #5786)) – Addresses cross-provider model ID matching, UUID serialization errors, and tool message sanitation for OpenAI-format agents.
- **fix(crons): record run timestamps in job timezone** (PR [#5783](agentscope-ai/QwenPaw PR #5783)) – Fixes Issue [#5779](agentscope-ai/QwenPaw Issue #5779) where cron state API returned UTC instead of the job’s configured timezone.
- **feat(memory): add auto-memory turn state management** (PR [#5777](agentscope-ai/QwenPaw PR #5777)) – Adds per-session auto-memory state tracking to `BaseMemoryManager`.

### 4. Community Hot Topics
The following Issues generated the most discussion (3+ comments) in the last 24 hours:

- **Issue [#5785](agentscope-ai/QwenPaw Issue #5785)** – *[Feature]: "I can't select hidden folders (starting with a dot) in coding mode."* (3 comments) – Highlights a missing UI affordance for selecting dot-directories, a common pain point for developers working with `.git`, `.env`, and other hidden configurations.
- **Issue [#5784](agentscope-ai/QwenPaw Issue #5784)** – *[Bug]: Frontend compression threshold shows wrong value for same model across providers* (3 comments) – A sharp catch by a user leveraging LLM-assisted code review; a matching fix is already in PR [#5786].
- **Issue [#5779](agentscope-ai/QwenPaw Issue #5779)** – *[Bug]: cron state API returns UTC time instead of job’s configured timezone* (3 comments) – A timezone correctness issue; fix is pending in PR [#5783].
- **Issue [#5770](agentscope-ai/QwenPaw Issue #5770)** – *[question]: "Hope the V2.0 official version surprises everyone! Looking forward!"* (3 comments) – A purely enthusiastic community sentiment, no technical content.

**Underlying need**: Users are actively **cross-referencing backend logic with frontend display**, demanding strict consistency in configuration (provider matching, timezone handling). There is also a strong expectation for **V2.0**—users are eager for the next major release.

### 5. Bugs & Stability
Seven bug reports were filed or updated today. Ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#5789](agentscope-ai/QwenPaw Issue #5789) | Context compression crashes when model output exceeds JSON Schema `maxLength`. Agent fails entirely. | No |
| **High** | [#5790](agentscope-ai/QwenPaw Issue #5790) | Loading animation (spinner) does not disappear after Agent response completes. User-facing UI freeze. | No |
| **Medium** | [#5787](agentscope-ai/QwenPaw Issue #5787) | Mobile webui bottom content truncated on all pages (tablet & phone). | No |
| **Medium** | [#5757](agentscope-ai/QwenPaw Issue #5757) | Feishu (Lark) channel: bot responds to first message only, then silently ignores all subsequent messages. | No |
| **Medium** | [#5782](agentscope-ai/QwenPaw Issue #5782) | Google Gemini embedding via OpenAI-compatible endpoint returns `index=None`, causing silent fallback to keyword search. | No |
| **Medium** | [#5784](agentscope-ai/QwenPaw Issue #5784) | Frontend compression threshold displays wrong value for same model ID across providers. | Yes (PR [#5786]) |
| **Low** | [#5779](agentscope-ai/QwenPaw Issue #5779) | Cron API returns UTC time instead of job-configured timezone. | Yes (PR [#5783]) |
| **Low** | [#5781](agentscope-ai/QwenPaw Issue #5781) | Offline coding mode cannot preview files because it requires online resource downloads. | No |

**Assessment**: The two **High** severity bugs (context compression crash and stuck loading animation) are the most critical, with no fix PRs yet. The **Medium** severity Feishu bot silence issue has persisted since July 3.

### 6. Feature Requests & Roadmap Signals
Two notable feature requests were submitted today:

- **Issue [#5785](agentscope-ai/QwenPaw Issue #5785)** – *Select hidden folders in coding mode.* Likely to be prioritized as a small UX fix for developer users.
- **Issue [#5780](agentscope-ai/QwenPaw Issue #5780)** – *Multi-user account management for team use.* This is a significant architectural request. The user explicitly states that the current "single Bot" model (where anyone can message the Bot) lacks team member management, role-based access, and per-user configuration.

**Prediction for next version (V2.0?):** The **multi-user account management** feature (Issue [#5780](agentscope-ai/QwenPaw Issue #5780)) aligns with typical V2.0 roadmaps for enterprise readiness. The **auto-memory turn state** feature (PR [#5777]) is likely to land in the next minor release (v1.1.13).

### 7. User Feedback Summary
- **Positive sentiment**: Issue [#5770](agentscope-ai/QwenPaw Issue #5770) expresses strong community excitement for V2.0 ("hope it surprises everyone").
- **Pain Points (UI/UX)**:
  - Mobile webui is broken (truncated content).
  - Loading spinner never stops after response.
  - Cannot select hidden folders in coding mode.
  - Skills list loads only 20 items; scroll-to-load-more is broken due to CSS `overflow` constraints.
- **Pain Points (Functionality)**:
  - Feishu bot stops replying after the first message (docker & hosted instances).
  - Context compression crashes on long model outputs.
  - Gemini embedding silently fails—vector search degrades to keyword search without user notification.
  - Offline mode is gated by online resource downloads.
- **Sentiment**: Users are actively **testing edge cases** (offline, mobile, multi-provider) and filing detailed root-cause reports, indicating a technically engaged user base that expects high reliability.

### 8. Backlog Watch
The following Issues/PRs require maintainer attention due to lack of response or age:

- **Issue [#5757](agentscope-ai/QwenPaw Issue #5757)** – *Feishu bot does not reply after first message* (Updated Jul 5, created Jul 3). Critical for enterprise users on the Feishu platform. **No maintainer response or fix PR.**
- **Issue [#5779](agentscope-ai/QwenPaw Issue #5779)** – *Cron API timezone bug* – A fix PR ([#5783](agentscope-ai/QwenPaw PR #5783)) exists but has not been merged.
- **Issue [#5789](agentscope-ai/QwenPaw Issue #5789)** – *Context compression JSON Schema crash* – Binary severity (crashes the agent), **no maintainer response or fix PR yet**.
- **PR [#5777](agentscope-ai/QwenPaw PR #5777)** – *Auto-memory turn state* – Submitted Jul 4, updated Jul 5, has no comments or reviews. Requires maintainer review to proceed.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for **2026-07-06**.

---

## ZeroClaw Project Digest — 2026-07-06

### 1. Today's Overview
The ZeroClaw project is experiencing a period of **high activity**, with 23 issues and 50 PRs updated in the last 24 hours. This signals a strong development push involving multiple core contributors. The primary focus is on closing out the **SOP (Standard Operating Procedure) control plane** milestone and finishing the **Goal Mode** implementation stack. There is also a significant uptick in **bug-fix PRs**, particularly around security hardening (authorization, path validation, secret handling) and runtime stability (zombie processes, hanging turns). No new releases were cut today, but the volume of merged work suggests a release may be imminent.

### 2. Releases
- **No new releases today.**
- The absence of a release despite high PR activity indicates the team is likely staging code for a **v0.8.4** or **Schema V4** release, given the extensive breaking changes in-flight (e.g., Schema V4 cut, compact skill injection).

### 3. Project Progress (Merged/Closed PRs)
Seven PRs were merged or closed today. Key changes:
- **[PR #8727](https://github.com/zeroclaw-labs/zeroclaw/pull/8727):** Security fix for the gateway—rejected empty bearer tokens.
- **[PR #8645](https://github.com/zeroclaw-labs/zeroclaw/issues/8645):** (Closed) Bug fix for persistent drift in the reload banner for `ZEROCLAW_*` env-overridden secrets.
- **[PR #8462](https://github.com/zeroclaw-labs/zeroclaw/issues/8462):** (Closed) RFC for runtime policy on OTel LLM and tool content was accepted and completed.
- **[PR #8251](https://github.com/zeroclaw-labs/zeroclaw/issues/8251), #7879, #7861, #8462:** Closed after implementation. These milestone issues for relationship memory, skill reflection, and security-audit visibility have been delivered.

### 4. Community Hot Topics
The most active discussions reflect deep architectural concerns and user onboarding friction:

- **[Issue #8681](https://github.com/zeroclaw-labs/zeroclaw/issues/8681):** Goal mode implementation split stack (8 comments). This tracker is coordinating the massive effort to split the `feat/goal-mode` branch into reviewable PRs. High risk and in-progress.
- **[Issue #6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165):** RFC for a lighter core (8 comments). The community is debating the boundary of ZeroClaw’s core vs. external integrations. This is a long-running, high-risk discussion that will shape the project's plugin architecture.
- **[Issue #8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603):** OpenAI Chat Completions adapter (3 comments). A user need for OpenAI API compatibility was escalated with a detailed RFC, indicating strong demand for interoperability with existing ecosystem tools.
- **Underlying needs:** The community is pushing for **improved interoperability** (OpenAI API adapter), **decoupled architecture** (lighter core via external integrations), and **better onboarding** (Android Termux setup, config template bugs).

### 5. Bugs & Stability
Several high-severity bugs were reported or fixed today:

| Severity | Issue | Problem | Fix PR Exists? |
| :--- | :--- | :--- | :--- |
| **S1 - Blocked** | [#8560](https://github.com/zeroclaw-labs/zeroclaw/issues/8560) | `browser_open` hangs agent turn when launcher fails (no display). | No |
| **S2 - Degraded** | [#8731](https://github.com/zeroclaw-labs/zeroclaw/issues/8731) | Stdio MCP servers accumulate as zombie processes under active daemon. | No |
| **S2 - Degraded** | [#8722](https://github.com/zeroclaw-labs/zeroclaw/issues/8722) | High-entropy detector redacts legitimate filenames. | No |
| **S2 - Degraded** | [#8718](https://github.com/zeroclaw-labs/zeroclaw/issues/8718) | `config init` ships a broken template that silently disables voice transcription. | No |
| **S2 - Degraded** | [#8733](https://github.com/zeroclaw-labs/zeroclaw/issues/8733) | models.dev catalog drops per-model vision capabilities. | No |
| **S2 - Degraded** | [#8720](https://github.com/zeroclaw-labs/zeroclaw/issues/8720) | Bedrock Nova 2 Lite caching error—user seeks config option to disable `cachePoint`. | No |

**Analysis:** The cluster of S2 bugs, especially the zombie MCP processes and the broken audio config template, represent **critical user experience and operational failures**. The missing fix for the hanging browser tool (S1) is a blocking workflow issue for headless users.

### 6. Feature Requests & Roadmap Signals
- **OpenAI API Adapter ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)):** This RFC is a strong signal that ZeroClaw aims to become a drop-in replacement for OpenAI endpoints. **Likely in next version.**
- **SOP Routing Fix ([#8719](https://github.com/zeroclaw-labs/zeroclaw/issues/8719)):** A user requested that a false `when` condition should advance to the next step, not end the run. This is a targeted enhancement to the SOP engine that is currently in-progress. **Likely in next version.**
- **Relationship Memory Workflows ([#8251](https://github.com/zeroclaw-labs/zeroclaw/issues/8251)):** Now closed, meaning the feature to surface relationship memory as user workflows has been delivered. This is a **significant milestone** for the memory system.
- **WASM Plugin Hooks ([#7822](https://github.com/zeroclaw-labs/zeroclaw/issues/7822)):** An RFC for sandboxed lifecycle hooks is gaining traction. This is a **longer-term architectural item** that enables a rich plugin ecosystem.

### 7. User Feedback Summary
- **Pain Point (High):** **Android/Termux installation is broken.** The installer misidentifies the architecture. User `state-space-swarm` is blocked.
- **Pain Point (High):** **Onboarding voice transcription is broken out of the box.** The `config init` command produces a config file that the daemon rejects, silently disabling audio. User `lynnkeele` reported a frustrating fresh install experience.
- **Frustration (Medium):** **Unmanageable branch count.** Contributor `Project516` pointed out 200+ stale branches clutter the repo, making collaboration harder.
- **Satisfaction (Low):** **Caching issues with Bedrock.** User `ngamradt` cannot disable a problematic caching feature via configuration, leading to random errors.
- **Satisfaction (Low):** **Security detections are too aggressive.** The high-entropy detector is frustrating users by redacting legitimate filenames, impacting tool output readability.

### 8. Backlog Watch
- **[Issue #7911](https://github.com/zeroclaw-labs/zeroclaw/issues/7911):** **Android Termux Setup (Open, Blocked).** Created 2026-06-18. No maintainer fix in sight. Needs `needs-author-action` label and `status:blocked`. This is a key platform gap.
- **[Issue #6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715):** **Delete unneeded branches (Open, Blocked).** Created 2026-05-16. Simple housekeeping task stuck in limbo.
- **[PR #8384](https://github.com/zeroclaw-labs/zeroclaw/pull/8384):** **Inkbox Channel (Open, needs-author-action).** Created 2026-06-27. A massive XL PR adding a native email/SMS/voice channel that is waiting on author action. Risk of going stale.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*