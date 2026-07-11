# OpenClaw Ecosystem Digest 2026-07-11

> Issues: 429 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-11 01:20 UTC

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

# OpenClaw Project Digest — July 11, 2026

## Today's Overview

The OpenClaw project is experiencing **high activity** with 429 issues and 500 pull requests updated in the last 24 hours, though no new releases were cut today. The issue tracker shows a healthy mix of open (232) and recently closed (197) items, while PRs skew toward open (314) versus merged/closed (186), indicating a significant review and merge bottleneck. **Severity concern**: two P0 issues remain open, one involving a critical gateway memory leak (RSS growing from 350MB to 15.5GB) and another affecting hosted Molty model selection. The project is actively processing community contributions across 20+ PRs today, with several high-impact fixes awaiting maintainer review.

## Releases

No new releases were published today. The latest stable release remains the prior version (v2026.5.18 referenced in issue #83959). No changelogs or migration notes to report.

## Project Progress

Today’s merged/closed PRs include several notable fixes:

- **#104030** *(fix(twitch): preserve UTF-16 pairs in outbound chunks)* — Closed. Prevents emoji corruption when Twitch text is split at hard boundaries.
- **#101433** *(fix(openai): map Responses refusal chunks during tool calls)* — Closed. Fixes generic tool-call failure when OpenAI emits refusal chunks during streaming.
- **#103300** *(fix: Feishu post messages truncate URLs containing underscores)* — Closed. Resolves long-standing issue (#41860) with underscore-containing URLs in Feishu messages.
- **#103367** *(fix(google): Veo video generation fails with google-prefixed model ids)* — Closed. Fixes API_KEY_INVALID errors when using Google Veo models.
- **#103714** *(fix(browser): closing a tab could destroy an unrelated live page when the target was an OOPIF iframe)* — Closed. Prevents accidental destruction of host pages when closing iframe targets.
- **#103874** *(fix(telegram): keep DM reply ids out of thread targets)* — Closed. Prevents Telegram DM reply IDs from being misinterpreted as topic IDs.

Key open PRs advancing toward completion:
- **#103998** *(fix(cli): avoid zero usage cost during cache refresh)* — Ready for maintainer look. Fixes `$0` display during cold cache rebuilds.
- **#103496** *(fix(skill-workshop): reject invalid proposal list limits)* — Ready for maintainer look. Enforces input validation on proposal limits.
- **#103408** *(fix(memory-wiki): prevent partial failures during concurrent agent writes)* — Ready for maintainer look. Critical fix for concurrent write races in Memory Wiki.
- **#89040** *(perf: avoid event-loop stall during embedded_run bootstrap-context)* — Ready for maintainer look. Eliminates 14-22 second stalls causing message loss.

## Community Hot Topics

### Most Active Issues (by comment count)

1. **[#99241 — Tool outputs render as image attachments (20 comments)](https://github.com/openclaw/openclaw/issues/99241)**  
   *Rating: 🐚 Platinum Hermit* — In long-running or ANSI-heavy workflows, tool results collapse into unreadable image placeholders. The agent loses access to stdout/stderr text. This is a **high-severity usability and reliability issue** for power users relying on verbose tool outputs.

2. **[#102175 — Embedded prompt cache breaks across boundaries (16 comments)](https://github.com/openclaw/openclaw/issues/102175)**  
   *Rating: 🦞 Diamond Lobster* — Regression where prompt cache continuity is lost across room_event, policy changes, queue reconstruction, and OpenAI Responses continuation. Affects long-lived embedded sessions with significant performance impact.

3. **[#10659 — Masked Secrets feature request (15 comments, 👍4)](https://github.com/openclaw/openclaw/issues/10659)**  
   *Rating: 🦞 Diamond Lobster* — Strong community demand for preventing agents from accessing raw API keys. Would protect against prompt injection and accidental credential leaks. Combines security with agent functionality.

4. **[#91588 — Gateway memory leak: 350MB to 15.5GB (15 comments)](https://github.com/openclaw/openclaw/issues/91588)**  
   *Rating: 🐚 Platinum Hermit* — **P0 critical**. Gateway process grows to 15.5GB RSS over 2-3 days, triggering OOM kills and restart cycles. This is the most severe stability issue in the project.

5. **[#63829 — Per-agent memory-wiki vault configuration (CLOSED, 13 comments, 👍10)](https://github.com/openclaw/openclaw/issues/63829)**  
   *Rating: 🦞 Diamond Lobster* — Closed feature request for isolated knowledge wikis per agent. Highly upvoted (10👍), indicating strong community desire for multi-agent knowledge isolation.

### Most Active PRs (by complexity/risk rating)

- **#89038** *(fix: skip setup-only channel plugins in outbound resolution)* — 🐚 Platinum Hermit, 🚨 compatibility and message-delivery merge risk. Critical fix for qqbot reconnect handling.
- **#89039** *(fix: prevent silent message loss from EmbeddedAttemptSessionTakeoverError)* — 🐚 Platinum Hermit, XL size. Addresses race conditions in session write locks during retry.
- **#89040** *(perf: avoid event-loop stall during embedded_run)* — 🐚 Platinum Hermit, XL size. Eliminates 14-22s stalls.

### Underlying Needs

The most commented issues reveal three core community needs: **reliability** (memory leaks, prompt cache breaks, session stalls), **security** (masked secrets, filesystem sandboxing), and **multi-agent isolation** (per-agent memory wikis, groupScope consolidation).

## Bugs & Stability

### Critical (P0)

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) 🐚 | Gateway memory leak: 350MB → 15.5GB RSS causing OOM kills and restart cycles | No fix PR linked |
| [#101763](https://github.com/openclaw/openclaw/issues/101763) 🦐 | Hosted Molty: model selector sends dotted ID (claude-opus-4.8) instead of dashed (claude-opus-4-8), breaking all agent replies | No fix PR linked |

### High (P1)

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#10659](https://github.com/openclaw/openclaw/issues/10659) 🦞 | Masked Secrets: agents can access raw API keys (security) | No fix PR |
| [#84569](https://github.com/openclaw/openclaw/issues/84569) 🦞 | WhatsApp session stalls on long model_call, messages lost | [#89039](https://github.com/openclaw/openclaw/pull/89039) (open, related) |
| [#83959](https://github.com/openclaw/openclaw/issues/83959) 🦞 | Codex app-server startup retries exhaust before replacement ready | No fix PR linked |
| [#87109](https://github.com/openclaw/openclaw/issues/87109) 🦐 | Gateway heap grows to 1073MB+ at idle on macOS, cron fails silently | No fix PR linked |
| [#99681](https://github.com/openclaw/openclaw/issues/99681) 🦞 | Discord plugin fails to auto-reconnect after 1006 WS close | Closed, no fix PR |
| [#40982](https://github.com/openclaw/openclaw/issues/40982) 🦞 | 3-minute no-output watchdog cap on CLI requests too aggressive | [#89040](https://github.com/openclaw/openclaw/pull/89040) (related, perf fix) |

### Regression (P2)

| Issue | Summary | Fix PR? |
|-------|---------|---------|
| [#102175](https://github.com/openclaw/openclaw/issues/102175) 🦞 | Prompt cache breaks across room_event, policy, Responses boundaries | No specific fix PR |

### Today's New Bug Reports (July 10-11)

- **#103934** *(overflow-recovery leaves unreachable transcript branches)* — Addressed by [#104034](https://github.com/openclaw/openclaw/pull/104034) (open fix)
- **#103882** *(zero usage cost during cache refresh)* — Addressed by [#103998](https://github.com/openclaw/openclaw/pull/103998) (ready for review)
- **#103802** *(ACP sessions fail when backend doesn't advertise thinking config)* — Addressed by [#103958](https://github.com/openclaw/openclaw/pull/103958) (open fix)
- **#103736** *(hot reload subsystems inconsistent during channel deferral)* — Addressed by [#103880](https://github.com/openclaw/openclaw/pull/103880) (open fix)
- **#103735** *(NO_REPLY sentinel with newline not stripped)* — Addressed by [#103835](https://github.com/openclaw/openclaw/pull/103835) (open fix)
- **#103712** *(closing OOPIF iframe destroys host page)* — Fixed by [#103714](https://github.com/openclaw/openclaw/pull/103714) (closed)

## Feature Requests & Roadmap Signals

### Most Requested Features (by comments & upvotes)

| Issue | Feature | Comments | 👍 | Traction |
|-------|---------|----------|---|----------|
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | Per-agent memory-wiki vault configuration | 13 | 10 | **CLOSED** — likely shipped or deferred |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets (prevent agent from seeing raw API keys) | 15 | 4 | Needs security review, product decision |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | Filesystem sandboxing config (tools.fileAccess) | 11 | 4 | Needs security review, product decision |
| [#7524](https://github.com/openclaw/openclaw/issues/7524) | groupScope option to consolidate group sessions into main | 6 | 4 | Needs maintainer review |
| [#6890](https://github.com/openclaw/openclaw/issues/6890) | Ralph Loop max iteration configuration per-agent | 6 | 3 | Needs maintainer review |
| [#8508](https://github.com/openclaw/openclaw/issues/8508) | Configurable/dynamic ack reaction emojis | 5 | 6 | Needs product decision |
| [#9409](https://github.com/openclaw/openclaw/issues/9409) | Better context overflow error messages | 8 | 3 | Needs product decision |

### Predictions for Next Release

Based on PR activity and maintainer attention signals:

1. **Memory leak fix** — The P0 gateway memory leak (#91588) is the most critical open issue. A fix is likely being prepared given the severity.
2. **Memory Wiki concurrency fix** — [#103408](https://github.com/openclaw/openclaw/pull/103408) is ready for review and addresses a multi-agent write race condition.
3. **Browser/Control UI features** — [#104012](https://github.com/openclaw/openclaw/pull/104012) (gateway browser panel for Control UI) and [#104033](https://github.com/openclaw/openclaw/pull/104033) (UI layout fix for narrow panes) suggest UI improvements are being prioritized.
4. **Google Meet enhancements** — Two PRs ([#103811](https://github.com/openclaw/openclaw/pull/103811), [#103719](https://github.com/openclaw/openclaw/pull/103719)) add full caption transcripts and fix English UI detection, suggesting meet integration is maturing.

## User Feedback Summary

### Pain Points
- **Memory leaks dominate dissatisfaction** — Multiple reports (P0 #91588, P1 #87109) describe the gateway consuming excessive memory and crashing silently. Users report "silent failure" of cron jobs under memory pressure (#87109), "repeated `launchd-handoff` restart cycles" (#91588).
- **Message loss is a recurring theme** — Issues #99241 (tool outputs as images), #84569 (WhatsApp stalls), #85714 (stranded final messages), #99681 (Discord reconnect failures) all describe scenarios where user messages or agent responses are lost without error.
- **Security concerns remain unaddressed** — Multiple open issues (#10659, #7722, #90684, #91283) request better security boundaries, with some (#10659) noting that "any agent can read your keys right now" via prompt injection.
- **Configuration complexity** — Feature requests for file access sandboxing (#7722), configPatch in plugin manifests (#6792), and default delivery targets (#9155) suggest users find configuration tedious and error-prone.

### Satisfaction Signals
- **High engagement on quality-of-life features** — The 6👍 on configurable ack reaction emojis (#8508) and 10👍 on per-agent memory wikis (#63829) show the community is actively invested in polish features.
- **Rapid bug fixing** — Several bugs reported within the last 1-2 days already have open fix PRs (#103934→#104034, #103882→#103998), indicating maintainer responsiveness.

## Backlog Watch

### Long-standing Issues Needing Maintainer Attention

| Issue | Age | Summary | Last Update | Status |
|-------|-----|---------|-------------|--------|
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 5+ months | Masked Secrets feature | Jul 11 | Needs product decision, security review |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | 5+ months | Filesystem sandboxing config | Jul 10 | Needs product decision, security review |
| [#7524](https://github.com/openclaw/openclaw/issues/7524) | 5+ months | groupScope option for group sessions | Jul 10 | Needs maintainer review |
| [#6890](https://github.com/openclaw/openclaw/issues/6890) | 5+ months | Ralph Loop max iteration config | Jul 10 | Needs maintainer review |
| [#8299](https://github.com/openclaw/openclaw/issues/8299) | 5+ months | Suppress sub-agent announce config | Jul 11 | Needs product decision |
| [#7669](https://github.com/openclaw/openclaw/issues/7669) | 5+ months | Re-enable dev channel npm distribution | Jul 10 | Needs maintainer review |
| [#6792](https://github.com/openclaw/openclaw/issues/6792) | 5+ months | configPatch in plugin manifest | Jul 10 | Needs product decision, security review |

### Long-standing PRs Needing Review

| PR | Age | Summary | Status |
|----|-----|---------|--------|
| [#89038](https://github.com/openclaw/openclaw/pull/89038) | 41 days | fix: skip setup-only channel plugins in outbound resolution | 👀 Ready for maintainer look |
| [#89039](https://github.com/openclaw/openclaw/pull/89039) | 41 days | fix: prevent silent message loss from EmbeddedAttemptSessionTakeoverError | 📣 Needs proof |
| [#89040](https://github.com/openclaw/openclaw/pull/89040) | 41 days | perf: avoid event-loop stall during embedded_run | 👀 Ready for maintainer look |
| [#90831](https://github.com/openclaw/openclaw/pull/90831) | 36 days | fix(control-ui): add tooltips for Thinking and Reasoning dropdowns | 📣 Needs proof |

**Notable**: The three PRs by Jerry-Xin (#89038, #89039, #89040) have been open for 41 days and address critical gateway stability issues (session takeover errors, event-loop stalls, outbound resolution). Despite being marked "ready for maintainer look," they remain unmerged, representing a significant risk to project stability.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided digest data.

---

## Cross-Project Ecosystem Comparison Report: AI Personal Assistant Agents

**Date:** 2026-07-11
**Scope:** OpenClaw, NanoBot, Hermes Agent, PicoClaw, NanoClaw, NullClaw, IronClaw, LobsterAI, TinyClaw, Moltis, CoPaw, ZeptoClaw, ZeroClaw

### 1. Ecosystem Overview

The open-source personal AI agent ecosystem is demonstrating **hyperactive, convergent development**, dominated by a handful of high-velocity reference implementations. The landscape is bifurcating between **large, generalist frameworks** (OpenClaw, Hermes, IronClaw) focused on multi-platform reliability and enterprise readiness, and **specialized or lightweight derivatives** (NanoBot, PicoClaw, ZeroClaw) optimizing for specific runtimes (local models, embedded systems, security). A clear "post-hype" phase is evident: the community is moving away from proof-of-concept features toward **stability engineering**—memory leak fixes, message delivery guarantees, session isolation, and security hardening. The most significant shared struggle across the board is **silent failure modes** (message drops, unlogged errors, zombie processes), indicating that the next competitive differentiator will be observability and deterministic reliability, not raw feature count.

### 2. Activity Comparison (Last 24 Hours)

| Project | Issues Updated | PRs Updated | New Release | Health Score (Qualitative) |
|---|---|---|---|---|
| **OpenClaw** | 429 | 500 | No | High — Very high activity; severe P0 memory leak |
| **NanoBot** | 7 | 42 | No | High — Active, focused iteration; security gap |
| **Hermes Agent** | 50 | 50 | No | High — Strong community; context compression advancing |
| **PicoClaw** | 2 | 18 | No | Moderate-High — Low merge rate (1/18) |
| **NanoClaw** | 25 (PRs only) | 25 | No | High — Internal sprint; lots of merged fixes |
| **NullClaw** | 2 | 0 | No | Low — Quiet; unaddressed security bug |
| **IronClaw** | 36 | 50 | No | Very High — Bug bash; Slack reliability crisis |
| **LobsterAI** | ? (17 PRs) | 17 | **Yes (v2026.7.10)** | High — Post-release stabilization |
| **TinyClaw** | 0 | 0 | No | Dormant |
| **Moltis** | 0 | 1 | No | Low — Stable but low community engagement |
| **CoPaw** | 44 | 49 | **Yes (v2.0.0)** | Very High — Major release; critical regressions |
| **ZeptoClaw** | 0 | 0 | No | Dormant |
| **ZeroClaw** | 20 | 50 | No | Very High — Major plugins infrastructure overhaul |

### 3. OpenClaw's Position

**Advantages:**
- **Scale of community engagement**: With 429 issues and 500 PRs updated in 24 hours, OpenClaw has the most active developer ecosystem by a wide margin. The volume of contributions alone creates a self-reinforcing moat.
- **Platform breadth**: Supports Twitch, Feishu, Telegram, Google Meet, Discord—far more channel integrations than Hermes (focused) or IronClaw (Slack-heavy).
- **Feature maturity**: Fixes for nuanced issues (e.g., UTF-16 emoji preservation, OOPIF iframe lifecycle) indicate deep platform-level engineering that smaller projects cannot match.

**Key Differentiator vs. Peers:**
- **Monolithic vs. modular**: Unlike ZeroClaw or PicoClaw (modular plugin architectures), OpenClaw is a core reference with a massive PR backlog. Its strength is integration testing, but its **2 P0 bugs** (gateway OOM, hosted model selector) undermine its reliability narrative.
- **Community size vs. IronClaw**: IronClaw matches OpenClaw's velocity (50 PRs vs 500) but with fewer total participants. OpenClaw's "long tail" of contributors is its strategic asset.

**Vulnerabilities:**
- The **PR merge bottleneck** (314 open vs 186 merged) is worse than any peer, risking contributor burnout.
- The P0 gateway memory leak (#91588) is the most severe unaddressed stability issue in the ecosystem.

### 4. Shared Technical Focus Areas

Several requirements are emerging independently across multiple projects, indicating deep technical gaps in the current state of the art:

| Need | Projects Affected | Evidence |
|---|---|---|
| **Message Delivery Reliability** | OpenClaw, NanoClaw, IronClaw, LobsterAI, ZeroClaw | Silent drops, false "delivered" flags, WhatsApp/Discord reconnect failures |
| **Memory/Context Management** | OpenClaw, Hermes, NanoClaw, IronClaw, CoPaw | Prompt cache breaks, context compaction bugs, concurrency races in shared memory |
| **Security Boundaries** | OpenClaw, PicoClaw, Hermes, NullClaw, ZeroClaw | Masked secrets request, MQTT TLS bypass, credential leakage to disk, A2A session isolation |
| **Multi-Agent Isolation** | OpenClaw, Hermes, LobsterAI, ZeroClaw | Per-agent wikis, separated context, profile overwrite bugs, cross-user A2A leaks |
| **Scheduled Task Reliability** | IronClaw, LobsterAI, ZeroClaw | Cron jobs failing, "No thread attached" errors, false delivery confirmations |
| **Plugin/Hardware Extensibility** | ZeroClaw, PicoClaw, OpenClaw | Plugin capability catalogs, outbound TCP/TLS, ARM builds, MCP registration stores |

### 5. Differentiation Analysis

| Dimension | OpenClaw / Hermes / IronClaw | NanoBot / PicoClaw / ZeroClaw | CoPaw / LobsterAI |
|---|---|---|---|
| **Architecture** | Monolithic core + channel adapters | Modular, plugin-driven | Application-specific (collaboration, enterprise) |
| **Target User** | Power users, self-hosters, developers | Local model users, edge/Raspberry Pi | Enterprise teams, knowledge workers |
| **Core Strength** | Platform breadth, integration testing | Security, lightweight runtime, i18n | Collaborative workflows, scheduled tasks |
| **Key Risk** | Merge bottleneck, memory leaks | Low merge rate, review bandwidth | Regression risk from major releases |
| **Differentiator** | Community scale, channel diversity | Plugin governance, sandbox security | Cowork modules, user profile management |

### 6. Community Momentum & Maturity

**Tier 1: Rapid Iteration (Release Weekly/Multiple PRs Daily)**
- **OpenClaw, IronClaw, ZeroClaw, CoPaw** — High PR volume, active bug bashes, multiple large features in flight. These are the projects driving the ecosystem's technical frontier.

**Tier 2: Stabilizing (Post-Release Bug Fixing)**
- **NanoClaw, LobsterAI** — Just shipped significant updates; focus on regression fixes and hardening. High signal-to-noise in activity.

**Tier 3: Sustained Active (Steady Feature + Fix Flow)**
- **NanoBot, Hermes Agent, PicoClaw** — Consistent daily activity, manageable backlogs. Hermes stands out for maintainer responsiveness to security issues.

**Tier 4: Low Activity / Dormant**
- **NullClaw, Moltis, TinyClaw, ZeptoClaw** — Minimal to no daily activity. NullClaw has a critical security issue with no maintainer response, which is a risk for any user depending on it.

### 7. Trend Signals

1. **Reliability is the new feature.** The most upvoted and commented issues are not about new models or plugins—they’re about messages not disappearing, memory not leaking, and agents not crashing. Projects that solve silent failure (delivery confirmations, observability, deterministic error handling) will win user trust.

2. **Security is becoming a product requirement, not just a concern.** The simultaneous emergence of "masked secrets" (OpenClaw), A2A session isolation calls (NullClaw), credential leakage fixes (Hermes), and MQTT TLS bypass fixes (PicoClaw) indicates that users are deploying agents in sensitive contexts and demanding cryptographic guarantees.

3. **Multi-agent orchestration is the next battleground.** Per-agent isolation, inter-agent collaboration (bus architectures), subagent delegation, and model overrides are appearing across OpenClaw, Hermes, NanoBot, ZeroClaw, and CoPaw. The killer app for these frameworks may be managing teams of agents, not single assistants.

4. **Local model integration is a painful gap.** NanoBot’s “+60 seconds per turn” Ollama experience and Hermes’ custom provider bugs suggest that the ecosystem is optimized for cloud APIs, not local inference. Projects that streamline local model setup (prompt caching, model auto-detection) have a differentiation opportunity.

5. **Platform consolidation pressure is mounting.** ZeroClaw's RFC to merge two WebSocket protocols and PicoClaw's push to unify iMessage backends suggest that architectural debt from early rapid growth is being recognized. The winners will be those who simplify their codebase, not just add features.

6. **The WhatsApp/Discord/Telegram "trilemma" remains unsolved.** No project has fully solved the reliability, UX (typing indicators), and bot command limitations across these three dominant chat platforms. This is a massive opportunity for a focused integration effort.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-11

## 1. Today's Overview
The project is in a highly active state, with **42 PRs** updated and **7 open issues** currently under discussion. This is a significantly above-average day for development velocity, driven largely by multiple contributors addressing core stability, performance, and feature gaps. Two security-adjacent issues were filed (the `/restart` authorization gap and sustained-goal blocking behavior), and maintainers are actively shepherding several large PRs—including memory consolidation fixes, exec session isolation, and subagent model overrides—through review. No new releases were published today.

## 2. Releases
No new releases today.

## 3. Project Progress
**17 PRs were merged or closed today**, representing substantial forward momentum:

- **Dream/Commit Hygiene** — PR #4873 (alekwo) closes issue #4872 by skipping no-op periodic commits in the Dream loop, preventing empty git commits.
- **WebUI Polish** — PR #4876 (chengyongru) guides queued prompts with a deliberate second Enter; PR #4877 adds lazy Prism syntax highlighting to file previews and diffs. Both merged.
- **Edit File Disambiguation** — PR #4635 (chengyongru) enforces exact `line_hint` consistency for `edit_file`, addressing the dominant failure mode in edit benchmarks; closed.
- **CLI Fix** — PR #4832 (m11y) handles CSI-u Shift+Enter escape sequences gracefully, fixing a regression from the multiline input feature.
- **Subagent Model Override** — PR #4623 (yu-xin-c) adds an optional `model` parameter to the `spawn` tool, enabling per-subagent model selection; closed (merged into feature branch).
- **Cron Model Presets** — PR #4622 (yu-xin-c) adds `model_preset` support for cron jobs, fixing #4378; closed.
- **Subagent Aggregated Results** — PR #4624 (yu-xin-c) introduces a configurable `subagentResultMode` with an `aggregated` option to buffer subagent outputs; feature branch progressed.

## 4. Community Hot Topics
- **Issue #4253 — Model Override Per Conversation** ([link](HKUDS/nanobot Issue #4253))  
  *6 comments, 0 reactions*: The most-discussed open issue. User `rombert` wants to switch between fast cloud models and private local models mid-conversation based on task sensitivity. The underlying need—**runtime model flexibility without global config changes**—is clearly high-value. Design discussion is focused on whether to use a `/model` slash command or extend existing config infrastructure. Maintainers appear to be leaning toward the latter, as evidenced by the merged subagent override and cron preset work.

- **Issue #4867 — Prompt Prefix Caching for Ollama** ([link](HKUDS/nanobot Issue #4867))  
  *3 comments, 0 reactions*: A follow-up to #2463. User `The-Markitecht` reports that NanoBot adds ~60 seconds per turn with Ollama local models due to prompt prefix divergence. This is a **performance-critical complaint**: the user explicitly calls the situation "totally unusable." This represents a real adoption blocker for local-model users. No fix PR exists yet.

- **Issue #4634 — Edit File Disambiguation (Closed)** ([link](HKUDS/nanobot Issue #4634))  
  *2 comments*: Closed after PR #4635 fixed the dominant failure mode in the edit benchmark. This was the most impactful issue resolved this week for agent reliability.

## 5. Bugs & Stability
| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **High** | #4776 — `/restart` authorization gap | Any paired user can DoS the entire bot process; no session-lock check. | No |
| **High** | #4879 (PR, open) — sustained-goal blocks interaction | Long-running background goals freeze the agent, preventing new user input. | PR #4879 (opt-in flag, default off) |
| **Medium** | #4860 — `nanobot onboard` command missing | New install via `uv tool install` ships no `onboard` or `webui` commands despite docs. | No |
| **Medium** | #4843 (PR, open) — MCP reconnect crash | AsyncExitStack cleanup during stale-stream reconnect crashes the gateway reconnection path. | PR #4843 fixes by deferring cleanup to shutdown |
| **Low** | #4835 (CLOSED) — WebUI queued message to wrong chat | First message on blank landing page can go to a different existing chat if user switches windows before new chat activates. | Closed, no PR noted |

The `/restart` issue (#4776) is notable: it represents an **unauthenticated process-kill vector**. The title claims it's a security finding, but no fix PR has been raised or even assigned.

## 6. Feature Requests & Roadmap Signals
**High-probability for next release (1–2 sprints):**
- **Per-conversation model override** (Issue #4253) — multiple users requesting; foundation exists in subagent/cron override work.
- **Model parameter for spawn tool** (Issue #4231) — merged in PR #4623; awaiting full release.
- **Dream commit conditionality** (Issue #4872) — fixed in PR #4873, merged.
- **Hook auto-discovery** (PR #4878) — opened today by KANG99; uses `pkgutil` scanning mirroring existing patterns.

**Lower probability / longer-term:**
- **A2A peer delegation** (PR #4571) — complex architectural change for agent-to-agent collaboration; only partially addresses #4179. Maintainers have several competing subagent/MCP proposals in flight.
- **Token compression for exec tool outputs** (PR #4588) — significant performance win but conflicts with other PRs in the same area.

## 7. User Feedback Summary
- **Pain Points:**
  - "The commands mentioned on the website don't exist" (#4860) — new-user onboarding friction.
  - "Extra 60 seconds to every single turn" with Ollama (#4867) — local-model experience is severely degraded.
  - "I would like to alternate [models] based on privacy requirements" (#4253) — power-user workflow blocked.
- **Satisfaction Signals:**
  - Deep engagement: 42 PRs updated in 24 hours suggests strong community contribution momentum.
  - The edit_file disambiguation fix (#4634 closed) directly addresses a long-standing reliability grievance.
- **Missing / Unaddressed Needs:**
  - No fix or maintainer response yet on the `/restart` security issue (#4776), authored 4 days ago.

## 8. Backlog Watch
- **Issue #4776 (Security: /restart authorization)** — 4 days old, no maintainer acknowledgment. Given the nature of the finding (unauthenticated DoS), this warrants expedited triage.
- **Issue #4867 (Ollama prompt caching)** — 1 day old, but a follow-up to #2463 which has been open much longer. The user reports this makes Ollama "totally unusable." If this issue represents a pattern of neglect on prompt performance, it could erode trust among local-model users.
- **PR #4205 (Mailbox-backed subagent results)** — 36 days old, open; conflicts with other subagent work. This PR competes with #4624's aggregated result mode. A maintainer decision on which approach to land would reduce contributor uncertainty.
- **PR #4588 (Token compression)** — 12 days open, conflicts pending resolution. High potential impact on token costs but appears stalled.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the structured project digest for **Hermes Agent** based on data from **2026-07-11**.

---

## Hermes Agent Project Digest — 2026-07-11

**Data Snapshot:** 50 active Issues | 50 active PRs | 0 New Releases

### 1. Today's Overview

The Hermes Agent project is experiencing **very high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. While no new releases were published, the community is deeply engaged in both bug reporting and feature development. Activity levels indicate a **healthy but strained** project state, with a surge of new contributions addressing long-standing architectural issues (e.g., two-phase context compression, per-profile browser concurrency) and critical stability bugs (TUI session staleness, Weixin delivery failures). The maintainers appear responsive, with several fix PRs already open for recently reported high-severity bugs.

### 2. Releases

No new releases were published on this date.

### 3. Project Progress

**Closed/Merged PRs (2):**
- **#62200** (CLOSED): `fix(gateway): notify home channels after supervisor restart` — Ensures Telegram/home channels receive a "back online" signal after a supervisor-driven restart (e.g., `systemctl restart`).
- **#62285** (OPEN, likely advancing): `fix(auth): make xAI OAuth pools multi-account resilient` — Addresses credential overwrite issues when adding multiple xAI OAuth accounts.

**Key Features/Progress in Open PRs (most likely to merge soon):**
- **#62389** ([PR](https://github.com/NousResearch/hermes-agent/pull/62389)): Implements the **prune-first phase** for context compression (#513), eliding old tool outputs on an absolute token budget without LLM calls. *Opt-in, backwards compatible.*
- **#62385** ([PR](https://github.com/NousResearch/hermes-agent/pull/62385)): Fixes gateway-executed cron job deadlocks by adding an env-gated escape hatch (`HERMES_CRON_DISABLE_IN_PROCESS`).
- **#62378** ([PR](https://github.com/NousResearch/hermes-agent/pull/62378)): Adds a fabrication-prevention block to the summarizer prompt to stop the LLM from inventing user requests during context compaction.
- **#62381** ([PR](https://github.com/NousResearch/hermes-agent/pull/62381)): Shares a single write-queue thread per database across agent and subagents, fixing concurrency issues with `RetainDBMemoryProvider`.

### 4. Community Hot Topics

The following issues and PRs generated the most discussion (by comment count or reactions):

- **#513** ([Issue](https://github.com/NousResearch/hermes-agent/issues/513)) — *Two-Phase Context Management*
  - **3 comments, updated today.** This Kilocode-inspired feature request continues to attract attention. A PR (#62389) implementing the first phase (prune tool outputs) was opened today, showing strong maintainer alignment with community demand.
- **#32107** ([Issue](https://github.com/NousResearch/hermes-agent/issues/32107)) — *Multiple users per agent with separated context*
  - **1 comment, but 7 👍 reactions.** This feature request for multi-user agent support (e.g., a startup embedding Hermes) has the highest positive reaction count in the dataset, indicating strong enterprise demand.
- **#52496** ([Issue](https://github.com/NousResearch/hermes-agent/issues/52496)) — *Dashboard rewrites custom provider to openrouter*
  - **7 comments.** Users are actively debugging a confusing UI bug where the dashboard corrupts custom provider configs. This is a high-friction issue for users relying on local/self-hosted LLMs.
- **#48098** ([Issue](https://github.com/NousResearch/hermes-agent/issues/48098)) — *Stale "Summarizing thread" status in Desktop*
  - **7 comments.** Persists as a major UX frustration; users report the desktop UI locking up visually while the model is actually working.

**Underlying Need Analysis:** The most active discussions reveal a community pushing for **enterprise-grade reliability and configurability**: multi-user support, robust context management, and UI indicators that accurately reflect backend state.

### 5. Bugs & Stability

**Critical/P1 Bugs (reported/updated today):**
- **#62170** ([Issue](https://github.com/NousResearch/hermes-agent/issues/62170)) — *TUI shows stale session content after switching sessions* (P2, needs-repro).
  - **Summary:** v0.18.1 TUI displays content from the wrong session after switching. A `fix` PR was filed today (likely related to session state risk).
- **#62383** ([Issue](https://github.com/NousResearch/hermes-agent/issues/62383)) — *Weixin iLink cron delivery fails with ret=-2 'rate limited' when context_token is stale* (P2).
  - **Summary:** Cron jobs fail silently due to misidentified session expiration. **Fix PR #62386** open today.
- **#62336** ([Issue](https://github.com/NousResearch/hermes-agent/issues/62336)) — *Terminal snapshots capture credential-bearing env vars to disk* (P3, Security).
  - **Summary:** Sensitive environment variables (API keys from Bitwarden) are persisted to disk during terminal environment snapshots. **Fix PR #62379** open today.
- **#62324** ([Issue](https://github.com/NousResearch/hermes-agent/issues/62324)) — *Desktop terminal fails to start due to missing execute bit on spawn-helper* (P3, duplicate).
  - **Summary:** A recent build change accidentally dropped the executable permission on `node-pty`'s helper binary.

**Regressions:**
- **#62369** ([Issue](https://github.com/NousResearch/hermes-agent/issues/62369)) — *Agent lacks time awareness in long sessions* (Feature, but indicates a design gap exposed by real usage).

**Overall Stability:** The project shows a high rate of bug reports related to **state management** (stale UI, stale sessions, persistence) and **security boundaries** (credential leakage, dangerous command bypass). Fix PRs are being opened promptly for most critical items.

### 6. Feature Requests & Roadmap Signals

**Top requested features (by community activity/reactions):**
- **Multiple users per agent with separated context** (#32107, 7 👍) — Strongest signal for a multi-tenant enterprise use case.
- **Volatile skills** (#36656, 2 👍, 2 comments) — Load skill content for one turn only to reduce context bloat.
- **Per-subagent model override in delegate_task** (#58731) — Fine-grained model routing for master-worker patterns.

**Likely candidates for next release (based on open PRs):**
1. **Two-phase context compression** (#62389) — The PR is already open and addresses a major cost/quality concern.
2. **True lightweight dashboard mode** (#61121) — A PR for memory-constrained self-hosted installs is advancing.
3. **OS theme auto-detection** (#59275) — Mid-session skin switching for TUI/CLI.
4. **Bounded/resumable desktop attachment uploads** (#62382) — Fixes a hard failure mode for large files.

### 7. User Feedback Summary

**Pain Points (explicit or inferred from bugs):**
- **Provider configuration is fragile:** (#52496, #52807) Users are frustrated that custom providers must be hand-edited in `config.yaml` and that the dashboard corrupts these settings.
- **Desktop/TUI reliability:** (#48098, #62170, #62324) Users report the UI frequently shows incorrect state (stale session, stuck "busy" indicator, terminal crashes).
- **Context management bloat:** (#513, #36656) Advanced users are hitting token limits and seeking smarter, cheaper compression strategies.
- **Security friction:** (#62336, #62388) Credentials leaking to disk and the restrictive approval system blocking legitimate cleanup operations are causing workflow interruptions.

**Satisfaction Signals:**
- High engagement (50+ PRs/Issues updated) indicates a very active and invested user base.
- Users are submitting detailed, well-structured bug reports and feature requests, suggesting commitment to the project.
- The existence of PRs for **#513** (two-phase compression) and **#32107** (multi-user) shows maintainers are listening to the community's deepest needs.

### 8. Backlog Watch

The following issues/PRs are long-standing and require maintainer attention:

- **#10835** ([Issue](https://github.com/NousResearch/hermes-agent/issues/10835)) — *Expose Hermes memory via MCP server* (CLOSED, but status is questionable; could be revisited).
- **#28156** ([Issue](https://github.com/NousResearch/hermes-agent/issues/28156)) — *Bedrock+Claude: wizard accepts Bearer-only setup, runtime fails* (P1, open since 2026-05-18). **5 comments, no fix PR.** This is the highest-priority bug that appears unaddressed; it blocks all Bedrock Claude users in EU regions.
- **#3630** ([Issue](https://github.com/NousResearch/hermes-agent/issues/3630)) — *Phase 4 — Advanced Security (Ephemeral Secrets, External Vaults)* (P3, opened 2026-03-28). No open PR. This long-standing security roadmap item has stalled.
- **#40077** ([Issue](https://github.com/NousResearch/hermes-agent/issues/40077)) — *Desktop app crashes on NVIDIA 580+ drivers* (P3, opened 2026-06-05). A fix PR (#39192) exists but remains open with no merge, suggesting a blocker or lack of testing capacity.
- **#45827** ([PR](https://github.com/NousResearch/hermes-agent/pull/45827)) — *fix(desktop): trim wrapper parens from raw URL autolinks* (P3, opened 2026-06-13). A minor but long-standing desktop UX fix awaiting review.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-11

## Today's Overview

The PicoClaw project shows **high development activity** with 18 pull requests updated in the last 24 hours, though only one was merged. Two new issues were filed today alongside one closure, and zero releases were published. The project's attention is concentrated on **security hardening, OAuth reliability, and WhatsApp UX improvements**. Several long-standing PRs remain open, indicating a backlog that may benefit from maintainer triage. Overall, the project is actively maintained with contributions from multiple community members, but the **low merge rate (1 of 18 PRs)** suggests review bandwidth may be a constraint.

## Releases

No new releases today. The latest release remains **v0.3.1** (no date available from current data). Users tracking the `dependabot` PRs may want to check the next release for updated dependencies including `eslint` and `mautrix`.

## Project Progress

**Merged/Closed Items (1):**
- **#3179** — `fix(whatsapp): reconnect after websocket drops` (by Alix-007). This PR reconnects the WhatsApp WebSocket bridge after read failures, configures read deadlines and ping/pong handlers, and dispatches inbound messages asynchronously. This addresses a **stale bug** originally filed in #3178.

**Notable Open PRs advancing features:**
- **#3242** — `feat(whatsapp): add native typing presence` (by greencabe). Implements `channels.TypingCapable` to send composing/paused states during reply processing.
- **#3241** — `fix(auth): make OAuth refresh provider-correct and concurrency-safe` (by greencabe). Direct fix for issue #3239.
- **#3246** — `fix: security and robustness hardening` (by corporatepiyush). Enables MQTT TLS verification, adds OAuth timeouts, and bounds search reads.
- **#3248** — `fix: bump Go to 1.25.12 to remediate stdlib vulnerabilities` (by afjcjsbx). Patches two `govulncheck` findings in `crypto/tls` and `os`.

## Community Hot Topics

1. **#2937 – Feat/agent collaboration** (by afjcjsbx)
   - *Status:* OPEN, updated 2026-07-10
   - *Summary:* Introduces a durable inter-agent communication bus with mailboxes, collaboration threads, permission-aware messaging.
   - *Analysis:* This is the **longest-running open feature PR** (since May 24). It represents a major architectural change. Community interest suggests high demand for multi-agent workflows. With no recent comments, it may need maintainer re-evaluation for inclusion in v0.4.0.

2. **#3240 – Add typing presence to WhatsApp native replies** (by greencabe)
   - *Status:* OPEN, filed 2026-07-10, 0 comments
   - *Analysis:* Filed alongside its fix PR (#3242). This issue received no comments but the PR is already open, indicating responsive development.

3. **#3239 – OAuth refresh requests use incompatible provider semantics** (by greencabe)
   - *Status:* OPEN, filed 2026-07-10, 0 comments
   - *Analysis:* Filed with fix PR #3241 already submitted. Demonstrates a **quick bug-to-fix turnaround** for critical auth infrastructure.

## Bugs & Stability

| Severity | Issue/PR | Description | Fix Status |
|----------|----------|-------------|------------|
| **Critical** | PR #3246 | MQTT channel hardcodes `InsecureSkipVerify: true` for all broker connections — no TLS verification | PR open, not merged |
| **Critical** | PR #3248 | Two Go stdlib vulnerabilities in `crypto/tls` and `os`: GO-2026-5856, GO-2026-4970 | PR open, not merged |
| **High** | Issue #3239 / PR #3241 | OAuth refresh sends incompatible payloads to OpenAI vs Google; includes fixed `scope` that can break refresh | PR open, not merged |
| **Medium** | #3178 (CLOSED) | WhatsApp WebSocket timeout — resolved by PR #3179 | Fixed and merged |

**Severity Assessment:** MQTT TLS bypass is a **security threat** for any deployment using MQTT channels. The stdlib vulnerabilities affect all installations. None of today's critical fixes have been merged yet.

## Feature Requests & Roadmap Signals

1. **WhatsApp native typing presence** — Issue #3240, PR #3242. Highly requested UX improvement for WhatsApp users. Likely in **next patch release**.

2. **Agent collaboration bus** — PR #2937. Not yet merged after 7 weeks. If prioritized, could be in **v0.4.0** but shows no recent activity.

3. **Simplex channel type** — PR #3193 (by dim). Adds a new communication channel. Sitting for 2 weeks without merge.

4. **Configurable default fallback chain** — PR #3200 (by lc6464). UI/UX feature for model fallback management. Stale for 10 days.

5. **Czech translations** — PR #3247 (by KrtCZ). Small i18n addition, likely low-barrier merge.

6. **Linux ARMv7 build target** — PR #3205 (by sarwonous). Enables PicoClaw on Raspberry Pi 3 B+ and similar devices. Addresses a real deployment gap.

**Prediction:** Typing presence (#3242) and security fixes (#3246, #3248) are most likely for the **next immediate release**. Agent collaboration (#2937) remains a major feature but appears stalled.

## User Feedback Summary

**Pain Points Identified:**
- **WhatsApp UX silence** — Users see no feedback between sending a message and receiving a reply (Issue #3240). Processing delays of several seconds feel broken without typing indicators.
- **Raspberry Pi deployment friction** — No ARMv7 build target forces manual compilation (PR #3205). This is a real blocker for edge deployments.
- **OAuth provider incompatibilities** — Users with OpenAI OAuth experience refresh failures due to hardcoded form-encoded payloads (Issue #3239).
- **WhatsApp disconnection fragility** — The WebSocket bridge would silently die on read failures, requiring manual reconnect (Issue #3178, fixed in PR #3179).

**Satisfaction Indicators:**
- Community contributors are actively submitting PRs (greencabe, corporatepiyush, Alix-007, afjcjsbx, others) — a sign of project health.
- Users are running PicoClaw in Docker on launchpad, with 9router gateways, and on Raspberry Pi — diverse deployment scenarios.

## Backlog Watch

| Issue/PR | Age | Priority | Reason for Attention |
|----------|-----|----------|---------------------|
| **#2937** – Agent collaboration | 48 days | **High** | Major feature PR; no comments from maintainers; may need design review or closure decision |
| **#1951** – Move install scripts to repo (by lc6464) | 109 days | **Medium** | Documentation infrastructure improvement; stale for months |
| **#3165** – Fix Seed XML tool calls (by Alix-007) | 17 days | **Medium** | OpenAI-compat provider fix for Volcengine Doubao; no maintainer response |
| **#3193** – Simplex channel (by dim) | 14 days | **Low-Medium** | New channel type; no review comments |
| **#3200** – Configurable fallback chain (by lc6464) | 10 days | **Medium** | UI feature with backend+frontend changes; stale |

**Maintainer Attention Needed:** PR #2937 (agent collaboration) is the highest-impact item needing either dedicated review, a maintainer decision to include in next milestone, or explicit closure with guidance. PR #1951 has been open for 109 days and should be triaged.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for **2026-07-11**.

---

## NanoClaw Project Digest: 2026-07-11

### 1. Today's Overview
The project is experiencing **peak activity**, with **25 PRs** updated in the last 24 hours—a significant surge suggesting a major internal sprint or "ship week." The core team is highly engaged, with core members (gavrielc, glifocat, amit-shafnir) driving a convergent push focused on **fixing timestamp consistency**, **unifying channel behavior**, and **implementing a new persistent memory system**. Bug severity is elevated, with two critical structural issues (#3001, #3002) regarding stale skill symlinks causing silent agent failures, though the team has responded rapidly with fix PRs. While there are no new releases, the volume and quality of merged PRs indicate a release candidate is likely imminent.

### 2. Releases
**None.** No new releases were created today. Given the high volume of closed PRs (10), a patch release bundling the **timestamp standardization** and **skill symlink fixes** is highly probable within the next 48 hours.

### 3. Project Progress (Merged/Closed PRs)
10 PRs were merged or closed today, indicating rapid stabilization of core infrastructure:

- **Timestamp Consistency (Critical Fix):** Three PRs (#3005, #3006, #3007) resolved a systemic bug where timestamps were stored in naive UTC but parsed as local time, causing hours-long rendering errors in chat histories and task logs. The new convention mandates ISO-Z UTC storage with local-time display.
- **Channel Architecture Refactor:** PRs #3009, #3010, and #3011 were merged, moving channel-specific formatting skills from the core trunk to a dedicated channels branch and implementing **adapter-declared channel defaults** (engage mode, threading, sender policies). This reduces hardcoded heuristics in the core engine.
- **Agent Safety & Tooling:** PR #3003 (docs) adds requirements for bounded waits in agent-browser scripts to prevent infinite loops. PR #3004 (closed) introduced a **Context Preview Tool** that allows developers to simulate agent scenarios and view the exact prompt sent to the LLM.
- **Codex Provider Fix:** PR #3000 fixed a token display bug in the Codex provider where the footer showed cumulative (thread-wide) token usage instead of per-turn values, resulting in "astronomical" numbers like 383M input tokens. It now prioritizes single-turn data.

### 4. Community Hot Topics

- **#2415 [CLOSED] - "Container config not found" on group create:** This bug generated significant concern as it blocks new agent group creation entirely. The CLI (bin/ncl groups create) skips inserting a required `container_configs` row, causing immediate spawn failure. It was closed, but no fix PR is explicitly linked, suggesting a hotfix.
- **#3001 [OPEN] - Stale shared skill symlinks:** This issue reveals a **silent data integrity problem**. Agent groups created before the shared-skills refactor (April 21) are permanently cut off from skill updates. The agent runs older skill content without any logging. This is the most dangerous open bug today due to its silent nature.
- **#2389 [CLOSED] - Messages silently dropped due to missing destinations:** A critical CLI bug where wirings created via `bin/ncl` did not auto-create `agent_destinations` rows. Agents generated responses but messages were swallowed. This was closed, likely resolved by a recent merge.

**Underlying Need:** The community is demanding **deterministic reliability** in agent setup and delivery. The common thread across these three issues is that the CLI and core database orchestration are inconsistent with the runtime expectations, leading to "silent failures" that are difficult to debug.

### 5. Bugs & Stability

| Issue | Severity | Status | Description | Fix PR Exists? |
| :--- | :--- | :--- | :--- | :--- |
| **#3001 - Stale skill copies** | **Critical** | **Open** | Pre-refactor groups ignore shared skill updates; silent failure. | **Yes** (#3002 partially addresses by adding warnings) |
| **#2415 - Missing container_configs** | High | Closed | CLI `groups create` skips DB insert, causing spawn failure. | Yes (assumed merged) |
| **#2389 - Missing destinations** | High | Closed | CLI `wirings create` does not create DB destinations, silent drop. | Yes (assumed merged) |
| **#3002 - Shared skill block** | Medium | **Open** (PR) | Real files in container dirs block symlinks. Fix adds warning log. | **Yes** (PR #3002 is the fix) |

**Assessment:** The project is currently battling a **class of silent bugs** related to database state inconsistencies. While PR #3002 adds a log warning for blocked symlinks, issue #3001 remains open, meaning affected users still need a manual migration path to repair their agent groups.

### 6. Feature Requests & Roadmap Signals

- **Provider-Agnostic Memory System:** The core team is actively working on this, with PRs #3012 and #3013 adding a persistent memory tree that loads on session start. This is a **major roadmap signal**, suggesting the next release will include shared, persistent memory that survives across agent sessions.
- **iMessage Channel Unification:** PR #2999 proposes merging two separate iMessage backends (local vs. hosted) into a single pluggable channel with skills. This signals a trend toward **channel modularity** and reducing maintenance burden.
- **Tasks: One-Door Delivery:** PR #2988 is part 3 of a "scheduled-tasks train." This refactors delivery to use explicit named destinations only, removing reply-in-place fallbacks. This suggests a major push toward **predictable, auditable message routing** for scheduled tasks.
- **Telegram Rich Rendering:** PR #2877 (still open) requests native rich message support using Bot API 10.1. This is a long-standing feature request for improved user experience on Telegram.

**Prediction:** The **persistent memory system** (PRs #3012, #3013) and the **adapter-declared channel defaults** (PR #3010) are strongest candidates for the next minor release.

### 7. User Feedback Summary

- **Pain Point: CLI Unreliability:** Users are frustrated that the primary CLI tool (`bin/ncl`) produces inconsistent database states. Issue #2415 ("first spawn fails") and #2389 ("messages silently dropped") indicate that the CLI is the weakest link in user onboarding.
- **Pain Point: Silent Agent Failures:** The community is deeply concerned about issues that fail without logging. Issue #3001 ("nothing in the logs says so") and #2389 ("silently swallowed") highlight a user demand for better observability.
- **Positive Signal: High Team Responsiveness:** Despite the high bug count, users see PRs merging within 24 hours of issue creation (e.g., the timestamp fixes). This indicates strong project velocity and maintainer attention.

### 8. Backlog Watch

- **#2877 - Telegram Rich Rendering (Open since 2026-06-28):** This PR has not received a core-team review or merge status update in 13 days. Given the concurrent push on iMessage and WhatsApp channel work, the Telegram channel may be deprioritized. **Action needed:** A maintainer should either assign a reviewer or request a rebase to prevent it from rotting.
- **#2966 - Agent Runner Logging (Open since 2026-07-06):** A fix for logging when errored batches are acked. This is a low-urgency but important observability improvement. It has 2 weeks of staleness with no comments from maintainers.
- **#3001 - Stale Skill Copies (Open, No Comments):** This is the highest-severity open bug. It was created yesterday, but with **0 comments**, it has not yet received a triage response from the core team confirming a fix timeline. Users impacted by this bug have no clear guidance. **Action needed:** Immediate triage confirmation.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-11

## Today's Overview
Project activity is low today, with no new releases, no pull requests, and only two open issues updated in the last 24 hours. The community is primarily focused on two unresolved bugs, one of which has been open for over a week and involves a core integration (Telegram). The second, filed yesterday, raises a potentially critical security concern in the A2A routing layer. No closed issues or merged PRs indicate a quiet day for development velocity, though the absence of new code contributions may signal maintainer attention is stretched.

## Releases
No new releases were made. The project remains on its previous version.

## Project Progress
No pull requests were merged or closed today. There is no evidence of recent feature advancement or bug fixes being integrated.

## Community Hot Topics
Two open issues are currently the focus of community attention:

- **Issue #972 — [bug] Telegram channel stops responding after idle time**  
  Author: i11010520 | Created: 2026-06-30 | Updated: 2026-07-10 | Comments: 2  
  [Link](https://github.com/nullclaw/nullclaw/issues/972)  
  The reporter describes that the Telegram integration becomes unresponsive after overnight idle periods, while the backend agent continues to function (responding to `ping`). The underlying need appears to be a connection keep-alive or reconnection mechanism for long-running Telegram sessions. No maintainer response yet.

- **Issue #974 — [BUG] NullClaw shared bearer A2A route allows cross-caller task and context reuse**  
  Author: N0zoM1z0 | Created: 2026-07-10 | Updated: 2026-07-10 | Comments: 0  
  [Link](https://github.com/nullclaw/nullclaw/issues/974)  
  The reporter describes a security vulnerability where multiple callers sharing a valid A2A bearer token can read and reuse each other's task history and context. This is a significant authority/access control issue in the agent-to-agent routing layer. No maintainer response yet.

## Bugs & Stability
| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| Critical | #974 | Shared bearer token allows cross-caller task/context reuse (security escalation) | No |
| High | #972 | Telegram channel dies after idle period, despite backend running | No |

The security bug (#974) is the most severe, as it implies a fundamental design flaw in A2A session isolation. No fix pull requests are currently open for either issue.

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the Telegram idle bug (#972) indirectly signals a need for:
- Automatic reconnection or heartbeat mechanism for persistent chat integrations
- Better idle-timeout handling in the Telegram channel adapter

The A2A security issue (#974) may drive architectural changes to session management — likely requiring per-caller session isolation or per-request authorization beyond bearer validation. These could appear in the next release if promptly addressed.

## User Feedback Summary
User feedback today is limited to bug reports:
- **i11010520** reports frustration with Telegram integration failing silently after idle periods, while backend remains functional. This suggests a missing watchdog or recovery path in the transport layer.
- **N0zoM1z0** raises a security concern that undermines trust in multi-user A2A setups. The detailed replay demonstrates a clear attack surface, indicating the reporter may be a security researcher or power user testing the project's boundaries. Satisfaction is likely low due to the lack of access controls.

Overall sentiment appears cautious, with two users encountering blockers in core functionality (chat reliability and security).

## Backlog Watch
No long-unanswered issues were identified beyond the two already discussed. However, Issue #972 (created 2026-06-30, 11 days ago without maintainer response) is becoming a stale open bug. If left unaddressed, it may discourage Telegram users and accumulate negative sentiment. Issue #974 (filed yesterday) should receive an initial maintainer acknowledgment soon, given its security implications.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-11

## Today's Overview

IronClaw remains in a **high-velocity development sprint**, with **50 PRs and 36 Issues updated in the last 24 hours** — indicating strong team and community engagement. The project is in the midst of a major **Reborn runtime transition**, with legacy v1 deprecation advancing alongside core resilience improvements. The **34 open PRs** (16 closed/merged) and **28 active Issues** suggest a healthy pipeline, though the **zero new releases** this period means fixes are piling up. Key themes include **loop execution hardening**, **MCP registration infrastructure**, **Slack integration stability**, and a coordinated **bug bash** surfacing user-facing issues.

---

## Releases

**None this period.** The last release appears to be the `0.29.1` / `ironclaw_common 0.5.0` prepared in PR #5598 (still open). No new versions were tagged today.

---

## Project Progress (Merged/Closed PRs Today — 16 items)

### Core Runtime & Resilience
- **#5960 (merged)** — Raised default loop iteration ceiling `32 → 256` to prevent mid-task fail-closure on tool-heavy turns. Addresses a root cause of silent failures.
- **#5895 (merged)** — Fixed compaction failures after successful tool results (#5838). Treats compaction errors as recoverable skip rather than terminal failure.
- **#5954 (merged)** — Phase 1 of `RunFailureReason` classification funnel: additive, zero behavior change, lays groundwork for structured error reporting.
- **#5844 (merged)** — Added "Computation" section to Reborn system prompt guiding the agent to use tools (not internal reasoning) for calculations.
- **#5817 (merged)** — Fixed decimal numbers being incorrectly flagged as capability IDs, which suppressed tool calls.

### Infrastructure & Build
- **#5967 (merged)** — Fixed boot crash-loop (#5966) where stale first-party manifest on persistent volume caused catalog load failure. Now skips invalid manifests gracefully.
- **#5950 (merged)** — Exposed production LocalDev capability-port assembly to integration tests (seam PR-A of harness-port plan).
- **#5499 (merged)** — WASM tool install from zip + env-provisioned tenant-shared credentials (foundational for configurable tools).
- **#5916 (closed)** — Per-user MCP registration store (superseded by #5970 on same feature, rebuilt on newer main).

### Minor Fixes
- **#5835, #5828, #5837, #5838, #4640** — Various bug bash issues closed (UI fixes, legacy test cleanup, Slack interaction fixes).

---

## Community Hot Topics

### Most Active Discussions

1. **#5948 — Bug Bash: GitHub extension activation false positive** (5 comments)
   - Assistant claims extension is "activated" when it's only installed; UI shows "Activate" button still visible.
   - **Link:** [Issue #5948](https://github.com/nearai/ironclaw/issues/5948)

2. **#5747 — No way to unpair Slack (closed)** (3 comments)
   - Users permanently locked into Slack pairing on `slack-v2-host-beta` with no disconnect path.
   - **Link:** [Issue #5747](https://github.com/nearai/ironclaw/issues/5747)

3. **#5891 — "Last completed" shows active run timestamp** (2 comments)
   - UI displays currently-running timestamp as "last completed" — misleading for users monitoring routines.
   - **Link:** [Issue #5891](https://github.com/nearai/ironclaw/issues/5891)

4. **#5741 — `builtin.http.save` fails with OutputTooLarge** (2 comments)
   - Tool fails when saving large web pages; no streaming or truncation support.
   - **Link:** [Issue #5741](https://github.com/nearai/ironclaw/issues/5741)

### Underlying Community Needs
- **Trust & accuracy:** Users need extensions' actual status (installed vs. activated) correctly reported — false positives erode trust.
- **Account control:** Locked Slack connections with no unpair path is a top pain point for users who need to switch accounts.
- **Robustness under load:** Tool failures on large outputs and compaction errors suggest users are pushing IronClaw beyond current limits.

---

## Bugs & Stability

### Severity P1 — Critical
- **#5943 — Slack DM posts to wrong channel instead of user DMs** — Message content leaks into shared channels.
- **#5944 — Slack DM delivery silently fails** — Run reports success but message never arrives.
- **#5945 — Long multi-tool runs fail with "model provider unavailable"** — Generic error after 34+ tool calls.
- **#5966 (fix: #5967, closed) — Boot crash-loop after #5499** — Stale manifest killed entire catalog load.

### Severity P2 — High
- **#5836 — Scheduled routines fail every 5 minutes ("No thread attached")** — 0% success rate on routine runs.
- **#5834 — Slack disconnect request incorrectly rejected** — Agent lies about inability to disconnect.
- **#5885 — Approval notification opens action without approval card** — Users cannot approve/deny.
- **#5879 — Stale error banner persists after successful follow-up** — UI pollution.
- **#5707 — Routine creation exposes internal implementation details** — Security concern, developer info visible to users.
- **#5946 — Assistant mutates Google Sheet before checking trigger availability** — Premature side effects.
- **#5955 — Multistep workflows with sub-agents fail** — Missions hit tool-call limit, stop progressing.

### Severity P3 — Medium
- **#5948 — GitHub extension false activation report**
- **#5891 — "Last completed" timestamp mismatch**
- **#5889 — "Load older messages" button non-functional**
- **#5947 — Thread deletion requires page refresh**

### Notable Regression Pattern
The **bug bash** (P2/P3 tags) has surfaced a **Slack integration reliability crisis**: DMs silently failing, misrouted messages, locked accounts, and agent incorrectly refusing disconnect requests. Fix PRs are in progress (#5959, #5965).

---

## Feature Requests & Roadmap Signals

### Clear Upcoming Features

1. **Per-user MCP Registration (PR #5970, open)** — Enables tenant-scoped MCP server registration. Likely next release (T1 of MCP stack; T2 egress, T3 registration API planned).

2. **Loop Resilience Overhaul (PR #5959, open)** — Deep availability retries, iteration backstop, model-visible tool-failure reasons. Directly addresses the 30% SWE-bench gap vs. competitors.

3. **Queued Message Steering (PR #5963, open)** — Allows users to send steering input to busy threads — significant UX improvement.

4. **Budget Approval Gate (PR #5964, open)** — Budget-as-blocked-resource with read-only usage settings — enterprise/admin feature.

5. **Retire v1 Runtime (Issue #5935)** — Remove legacy `src/` code, retarget CI/Docker/docs to Reborn. Major architectural milestone.

### Community-Requested Features
- **#5953 — Channel disconnect for non-Slack ExternalChannel extensions** — Extension removal doesn't cleanly disconnect.
- **#5968 — HTTP tool fails with third-party APIs without MCP** — Users want generic API connectivity.
- **#5969 — GLM-5.2 not in opencode default model list** — Users need manual config for new models.

### Prediction for Next Version
Next release will likely include: MCP registration store (#5970), compaction fix (#5895), loop ceiling raise (#5960), and the RunFailureReason funnel (#5954). The queued-message/budget stack (#5962/#5963/#5964) may land in the following release.

---

## User Feedback Summary

### Pain Points
- **Slack integration is unreliable** — DMs fail silently, messages go to wrong channels, accounts get locked with no unpair path. Highest frustration signal.
- **Long-running workflows break unpredictably** — 34+ tool calls trigger "model provider unavailable" — users lose work.
- **Scheduled routines don't work** — "No thread attached" every 5 minutes; routine feature is effectively broken.
- **UI feedback is misleading** — Stale error banners, incorrect "completed" timestamps, non-functional buttons erode confidence.
- **Side effects before validation** — Assistant modifies Google Sheets before verifying Slack trigger availability — destructive behavior.

### Positive Signals
- **Active bug bash engagement** — Multiple users filing detailed, reproducible reports with screenshots and steps.
- **SWE-bench gap analysis is driving platform improvements** — Team is methodically addressing the 30% gap vs. Hermes/OpenClaw (PR #5959).

### Dissatisfaction Indicators
- Routine reliability (Issue #5836) — 0% success rate is a **critical user-facing failure** for automation users.
- Approval flow (Issue #5885) — Notifications that open to blank approval cards constitute a **blocked workflow**.

---

## Backlog Watch

### Issues Needing Maintainer Attention

1. **#5741 — `builtin.http.save` OutputTooLarge** (created Jul 6, 2 comments, no fix PR)
   - Users cannot save large web pages; basic tool functionality broken.
   - [Issue #5741](https://github.com/nearai/ironclaw/issues/5741)

2. **#5640 — Harness gap: no RecordingSecurityAuditSink** (created Jul 4, 2 comments, no fix PR)
   - Integration harness cannot reproduce production security audit behavior — gap in test coverage.
   - [Issue #5640](https://github.com/nearai/ironclaw/issues/5640)

3. **#5860 — Tool activity details only appear after completion** (created Jul 9, 2 comments, no fix PR)
   - Users cannot inspect running tool calls — debugging blocked.
   - [Issue #5860](https://github.com/nearai/ironclaw/issues/5860)

### PRs Needing Review
- **#5780 — Admin installed and private skills** (created Jul 7, open, 0 comments) — Large feature adding skill management; stalled.
- **#5926 — Dependabot bulk update** (20 dependencies, including breaking `agent-client-protocol` 0.10.4→1.2.0) — Needs careful review.

### Long-Standing Watch Item
- **#4640 — Google Calendar list_events returns unordered/oldest events** (created Jun 9, closed today but fix only recently merged) — Took 1 month to resolve; suggests slow response on extension bugs.

---

*Report generated from IronClaw GitHub data for 2026-07-11. All links point to `github.com/nearai/ironclaw`.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the **LobsterAI Project Digest** for **2026-07-11**, generated from the provided data.

---

### 1. Today's Overview

LobsterAI is in a high-velocity phase today, with **17** PRs updated and a new release (`2026.7.10`) pushed. The balance is strongly skewed toward maintenance and stability, with **10** PRs merged/closed and only **7** still open. The project’s focus is on fixing critical regressions in the Cowork module (queues, follow-ups, permission prompts) and resolving IM routing issues for scheduled tasks. While activity is high, a significant community bug regarding agent configuration overwriting (Issue #2293) remains unresolved, indicating a potential point of friction for multi-agent users.

### 2. Releases

**New Version: `LobsterAI 2026.7.10`** (Released 2026-07-10)

- **Key Changes:**
    - **Agents:** Support for delegated subagent collaboration (PR #2285).
    - **Cowork:** Added minimizable permission prompts to improve user experience during long-running workflows (PR #2296).
- **Migration Notes:** No breaking changes or specific migration instructions were noted in the release notes.

### 3. Project Progress

The **10 closed/merged PRs** today demonstrate a heavy focus on fixing the Cowork experience and scheduled task reliability.

- **Cowork (Collaboration):**
    - **Context:** Merged support for folder context attachments (PR #2310).
    - **Queuing:** Fixed the submission logic for selected queued steer to preserve FIFO processing (PR #2313).
    - **Follow-ups:** Fixed the connection of queued follow-up coordinators when the app is minimized or across sessions (PR #2315).
    - **State:** Fixed state loss when the "Ask User" prompt is minimized (PR #2312).
- **Scheduled Tasks:**
    - Repaired IM group task routing, filtering targets by the correct bot/agent binding (PR #2306).
    - Fixed a casing issue for WeCom and DingTalk group IDs, ensuring delivery targets remain case-sensitive (PR #2314).
- **Memory & Indexing:**
    - Fixed migration for FTS-only memory indexes, ensuring all configured agents are reindexed safely on startup (PR #2311).
- **Build & UI:**
    - Fixed Windows title bar logo compression (PR #2316).
    - Fixed ES2020 compatibility for null-byte stripping in the build process (PR #2309).

### 4. Community Hot Topics

The most active discussion revolves around a user-reported bug regarding multi-agent profile management.

- **Issue #2293: [OPEN] Multi-Agent USER.md Overwrite Bug**
    - **Summary:** A user reports that modifying the "About You" settings or `USER.md` for one agent causes the same file to be overwritten in all other agents. The user identifies this as a recent regression after an update.
    - **Comments:** 3
    - **Link:** [Issue #2293](https://github.com/netease-youdao/LobsterAI/issues/2293)
    - **Analysis:** This is a high-impact bug for users managing multiple distinct agents (e.g., different personalities or roles). The user suspects it's a synchronization/storage logic error introduced recently. The maintainers have not yet acknowledged or assigned the fix.

### 5. Bugs & Stability

- **HIGH SEVERITY: Multi-Agent Profile Overwrite (Issue #2293)**
    - **Reported:** A user confirmed that `USER.md` files for individual agents are replaced by the main agent's content upon restart.
    - **Status:** Open, unassigned.
    - **Fix PRs:** None detected.

- **MEDIUM SEVERITY: Scheduled Task Toggle Not Responding (Issue #1392)**
    - **Reported:** A user found that the on/off toggle for certain scheduled tasks does not work.
    - **Status:** Closed (stale), likely resolved in a prior release.
    - **Fix PRs:** None detected in this batch.

- **LOW SEVERITY: Cron "delivered=true" False Positive** (Related to PR #2314)
    - **Reported (via PR context):** QA found that DingTalk connector swallows text API failure responses, causing the cron job scheduler to display a false "delivered" status.
    - **Status:** Fixed in the merged PR #2314.

### 6. Feature Requests & Roadmap Signals

Several user-requested features in the backlog have associated open PRs, suggesting they are in active development or review.

- **Session List Organization (Issue #1337 / PR #1338):** Users want the session sidebar grouped by time (Today, Yesterday, This Week). A PR (#1338) implementing this has been open since April. Given the high user visibility, this is a strong candidate for the next major feature release.
- **Workdays Schedule for Tasks (PR #1335):** A feature to select "Mon-Fri" only for scheduled tasks has a pending PR. This is a likely addition to the scheduled task module.
- **MCP JSON Import (PR #1336):** Allowing users to paste JSON to configure custom MCP servers instead of manual entry. This is a popular developer-focused feature request with an open PR.
- **Error State Indicators (Issue #1330 / PR #1331):** Adding a red dot to sessions in an error state in the sidebar. Another feature with an open PR, waiting for merge.

### 7. User Feedback Summary

- **Pain Points:**
    - **Profile Isolation (Critical):** The ability to maintain distinct, isolated personalities for multiple agents is broken. This is a core workflow blocker for advanced users.
    - **Task Management (Medium):** The scheduled task toggle issue (stale) shows that users rely heavily on the task system and are sensitive to UI/UX glitches.
- **Use Cases:**
    - Users are clearly managing multiple agents for different purposes (work, personal, specific projects).
    - Users are heavily utilizing the scheduled task system for automating routines.
- **Satisfaction:**
    - The volume of fixes for the Cowork module (queuing, context, state) suggests developers are actively addressing user feedback about the collaboration features, which is a positive signal.

### 8. Backlog Watch

The following items have been open for over three months without resolution or acknowledgment from maintainers, posing a risk to project health.

- **Bug: Scheduled Task Toggle Not Working (Issue #1392)**
    - **Status:** CLOSED (Stale). The issue was closed by the stale bot, but it is unclear if a permanent fix was deployed. This may re-occur for users.
    - **Link:** [Issue #1392](https://github.com/netease-youdao/LobsterAI/issues/1392)

- **Feature PR: Session List Time Grouping (PR #1338)**
    - **Status:** OPEN (Stale). A high-visibility UX improvement that has been ready for review since April.
    - **Link:** [PR #1338](https://github.com/netease-youdao/LobsterAI/pull/1338)

- **Feature PR: Custom MCP Server JSON Import (PR #1336)**
    - **Status:** OPEN (Stale). A significant feature for power users that remains unmerged.
    - **Link:** [PR #1336](https://github.com/netease-youdao/LobsterAI/pull/1336)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-11

## 1. Today's Overview
The Moltis project shows minimal activity over the past 24 hours: no new releases were published, no issues were updated, and only one pull request (#1146) saw a status update. The single open PR proposes adding GPT-5.6 model support, indicating that the team is preparing for a new model integration but has not yet merged the change. Overall, the project appears to be in a low-activity phase with no signs of urgent bugs or community friction. The absence of open issues or recently closed issues suggests stable operation with no active user-reported problems.

## 2. Releases
**No new releases** were published in the last 24 hours or in the recent history. The latest release information remains unavailable. No migration notes or breaking changes to report.

## 3. Project Progress
- **No merged or closed PRs** in the last 24 hours.  
- The only active PR (#1146) remains open and unmerged, so no features or fixes have advanced to completion today.

## 4. Community Hot Topics
The only active item is:

- **[PR #1146 – Add GPT-5.6 model support](https://github.com/moltis-org/moltis/pull/1146)**  
  *Author: PeterDaveHello | Created: 2026-07-09 | Updated: 2026-07-10*  
  This pull request proposes adding GPT-5.6 Sol, Terra, and Luna models to the OpenAI and OpenAI Codex fallback catalogs, including correct context window limits (1.05M for OpenAI API, 372K for ChatGPT/Codex backend). It also replaces superseded model references in documentation.  
  **Underlying need:** Users likely require support for the latest GPT-5.6 variants to leverage improved context handling and model capabilities. The fact that this PR has zero comments or reactions suggests the community has not yet engaged with it, possibly because it was only recently opened.

## 5. Bugs & Stability
**No bugs, crashes, or regressions** were reported in the last 24 hours. The issue tracker shows zero open or closed issues, indicating no stability concerns are currently active. This suggests a stable release cycle with no urgent fixes needed.

## 6. Feature Requests & Roadmap Signals
- **GPT-5.6 support (PR #1146)** is the only feature signal visible today.  
  **Prediction:** If merged, this feature is likely to appear in the next minor release (v1.x.x or equivalent). Given that GPT-5.6 models already have defined API context windows and fallback behavior, the implementation appears mature and ready for inclusion. No other feature requests were detected in the data.

## 7. User Feedback Summary
There are no user comments, reactions, or issue discussions in the last 24 hours to analyze. The project shows no active pain points or satisfaction signals. This could indicate either a satisfied user base or low community engagement at this time.

## 8. Backlog Watch
- **No long-unanswered issues or PRs** require maintainer attention. The single open PR (#1146) is only 2 days old and has not yet been reviewed or commented on by maintainers.  
- The issue tracker is completely empty, so there are no neglected items in the backlog. **No action required** for backlog cleanup.

---

**Overall Project Health:** 🌿 Stable / Low Activity — No bugs, no community friction, and a single pending feature addition. The project appears well-maintained but currently in a quiet period.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the provided GitHub data for the CoPaw project (aliased as QwenPaw in the data), here is the project digest for **2026-07-11**.

---

## CoPaw Project Digest — 2026-07-11

### 1. Today's Overview
CoPaw is experiencing a major milestone release with **v2.0.0** going stable, accompanied by an intense day of post-release stabilization. Activity is extremely high, with 44 issues and 49 PRs updated in the last 24 hours, indicating a robust community and development velocity. The project successfully merged the foundational **Runtime 2.0** migration from AgentScope 1.x to 2.0, but this has introduced several critical regressions in memory, MCP access control, and sandbox stability that are now being actively patched. The release verification process is ongoing.

### 2. Releases
Three releases were created, culminating in a major version bump:
- **v2.0.0 (Stable)**: The primary release featuring **Runtime 2.0**, a kernel refactor based on AgentScope 2.0.
- **v2.0.0-beta.7 & v2.0.0-beta.6**: Pre-release candidates that fixed memory session propagation (`session_id`) and envelope error state handling.

**Breaking Changes & Migration Notes:**
- **Breaking Change:** The backend has been migrated from AgentScope 1.x to AgentScope 2.0 ([#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727)). Users upgrading from v1.x should expect API changes and potential incompatibility with existing configurations.
- **Known Migration Bug:** Users upgrading to v2.0.0 may encounter a critical sandbox issue on Windows where `icacls` timeout causes recursive PowerShell processes and memory exhaustion ([#5951](https://github.com/agentscope-ai/QwenPaw/issues/5951)).
- **Module Import Error:** A bug exists where auto-memory fails due to a missing module (`agentscope.tool._builtin._scripts`) ([#5952](https://github.com/agentscope-ai/QwenPaw/issues/5952)).
- The community is explicitly requesting a formal upgrade guide to address these breaking changes and data compatibility concerns ([#5948](https://github.com/agentscope-ai/QwenPaw/issues/5948)).

### 3. Project Progress
The following key PRs were merged or closed today, advancing features and fixing critical issues:
- **Core v2.0.0 Release**: PR [#5942](https://github.com/agentscope-ai/QwenPaw/pull/5942) bumped the version to v2.0.0.
- **Memory Fix**: PR [#5938](https://github.com/agentscope-ai/QwenPaw/pull/5938) fixed a critical bug where `session_id` was not propagated into ReMe summarize tasks, causing memory attribution failures.
- **Documentation & Website**: PR [#5940](https://github.com/agentscope-ai/QwenPaw/pull/5940) updated the homepage for the v2.0 launch, and PR [#5932](https://github.com/agentscope-ai/QwenPaw/pull/5932) updated core documentation.
- **Regression Fix Revert**: PR [#5936](https://github.com/agentscope-ai/QwenPaw/pull/5936) reverted an earlier time-injection feature due to a poor display implementation.
- **Tool Result Fix**: Open PR [#5953](https://github.com/agentscope-ai/QwenPaw/pull/5953) addresses a major bug where truncated tool results caused agents to incorrectly trigger `recall_history` calls.

### 4. Community Hot Topics
The most active discussions highlight immediate post-release pain points:
- **[#5951](https://github.com/agentscope-ai/QwenPaw/issues/5951) (OPEN)**: "Desktop shell sandbox: icacls timeout silently swallowed → pwsh recursive explosion + 20GB memory." This is the most urgent issue, describing a total system failure on Windows. The user is demanding a rollback to v1.1.12.
- **[#5947](https://github.com/agentscope-ai/QwenPaw/issues/5947) (OPEN)**: "V2.0.0版本 MCP中禁用了某些子工具的访问,但是agent还是可以调用. 允许和拒绝失效." An MCP access control regression where deny rules are ignored. A fix is already available in PR [#5949](https://github.com/agentscope-ai/QwenPaw/pull/5949).
- **[#5945](https://github.com/agentscope-ai/QwenPaw/issues/5945) (OPEN)**: A user celebration thread for the v2.0.0 release, indicating high community anticipation.
- **[#5946](https://github.com/agentscope-ai/QwenPaw/issues/5946) (OPEN)**: A bug where truncation hints cause agents to falsely believe content is missing and initiate unnecessary `recall_history` calls, wasting tokens.

### 5. Bugs & Stability
Several critical regressions have been introduced with the v2.0.0 release. Ranked by severity:

- **CRITICAL - Windows Sandbox Broken**: [#5951](https://github.com/agentscope-ai/QwenPaw/issues/5951): Recursive PowerShell processes and memory exhaustion render the tool unusable on Windows. No fix PR is yet associated.
- **HIGH - MCP Access Control Broken**: [#5947](https://github.com/agentscope-ai/QwenPaw/issues/5947): Agent ignores user-configured tool deny rules. Fix PR [#5949](https://github.com/agentscope-ai/QwenPaw/pull/5949) is open and under review.
- **HIGH - Auto-Memory Module Error**: [#5952](https://github.com/agentscope-ai/QwenPaw/issues/5952): Memory summarization fails completely on all agents due to a missing import.
- **HIGH - Schema Error on `/mission`**: [#5918](https://github.com/agentscope-ai/QwenPaw/issues/5918): The mission workflow enters an infinite loop due to a `prd.json` format error.
- **MEDIUM - False Doom Loop Detection**: [#5906](https://github.com/agentscope-ai/QwenPaw/issues/5906): The anti-repetition feature falsely triggers, halting valid conversations.
- **MEDIUM - Iteration Counter Bug**: [#5896](https://github.com/agentscope-ai/QwenPaw/issues/5896): The max iteration limit resets incorrectly, forcing users to re-ask questions prematurely.

### 6. Feature Requests & Roadmap Signals
The community is actively requesting enhancements alongside the stability fixes:
- **Session Management**: [#5903](https://github.com/agentscope-ai/QwenPaw/issues/5903) requests session grouping for organization and import/export functionality. A design proposal PR [#5943](https://github.com/agentscope-ai/QwenPaw/pull/5943) has been opened, suggesting this could land in the next minor release.
- **LaTeX Rendering**: [#5453](https://github.com/agentscope-ai/QwenPaw/issues/5453) requests KaTeX support in the desktop app for rendering mathematical formulas.
- **Configurable Themes**: A design proposal ([#5909](https://github.com/agentscope-ai/QwenPaw/issues/5909)) for a configurable theme/skin module is under discussion, indicating planned UI customization improvements.
- **Vision Fallback**: PR [#5726](https://github.com/agentscope-ai/QwenPaw/pull/5726) (open) aims to implement automatic fallback to a vision-capable model when the primary model is text-only—a feature likely to be merged for a future beta.

### 7. User Feedback Summary
- **High Satisfaction with v2.0.0 Release**: Users are celebrating the launch (#5945), but this is immediately tempered by significant regression pain.
- **Key Pain Points**:
    - **Windows Sandbox Regression**: The most severe complaint, with a user reporting the tool is "almost unusable" and demanding a rollback to v1.1.12.post3.
    - **Lack of Upgrade Guidance**: Users upgrading from v1.x are confused about breaking changes, data compatibility, and migration steps ([#5948](https://github.com/agentscope-ai/QwenPaw/issues/5948)).
    - **False Positives in Safety Features**: Both the "Doom loop" detection and the "recall_history" tool result hints are causing unnecessary friction and breaking user workflows.

### 8. Backlog Watch
- **High-Impact Open Issue**: [#5856](https://github.com/agentscope-ai/QwenPaw/issues/5856) (OPEN, 3 comments): "Tool_call structure lost during context compaction, causing 400 errors." This is a structured data loss bug that can corrupt an agent's reasoning context and has been open for 2 days without a linked fix PR. Maintainers should prioritize this.
- **Stale Long-Tail Bugs**: Issues [#3502](https://github.com/agentscope-ai/QwenPaw/issues/3502) (WeChat Work connection instability) and [#3432](https://github.com/agentscope-ai/QwenPaw/issues/3432) (Lark integration permission failures) remain closed but unresolved, suggesting these channels may not be a current focus.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-11

## Today's Overview

The ZeroClaw project shows **high development activity** on 2026-07-11, with 50 pull requests updated in the last 24 hours (46 open) and 20 issues updated (17 open/active, 3 closed). The team is pushing forward a **major plugins infrastructure overhaul** spanning raw TCP/TLS outbound connections, a unified capability catalog, and webhook verification handshakes — all stacked across multiple interrelated PRs. Two **S1 (workflow blocked) severity bugs** were reported today: Gemini function calls failing due to a dropped `thought_signature` field, and Telegram bot command registration breaking when tool counts exceed 100. No new releases are recorded for this date.

## Releases

**No new releases** for 2026-07-11. The last recorded release remains v0.8.2; the v0.8.3 tracking issues (observability [#8073](https://github.com/zeroclaw-labs/zeroclaw/issues/8073), config-driven policy [#8363](https://github.com/zeroclaw-labs/zeroclaw/issues/8363)) are actively accumulating work.

## Project Progress

**3 issues closed** in the last 24 hours:
- [#8397](https://github.com/zeroclaw-labs/zeroclaw/issues/8397) — Feature: Expose `uses_memory` flag in CLI and cron tools (enhancement, closed 2026-07-10)
- [#8677](https://github.com/zeroclaw-labs/zeroclaw/issues/8677) — Feature: Add uses_memory checkbox to web gateway (closed 2026-07-10)
- [#7809](https://github.com/zeroclaw-labs/zeroclaw/issues/7809) — Bug: Channel turns ignore runtime-profile strict/parallel tool flags (closed 2026-07-10)

**4 PRs merged/closed** in the last 24 hours (full list of 50 PRs, 46 open). Notable feature-advancing open PRs include:
- [#8948](https://github.com/zeroclaw-labs/zeroclaw/pull/8948) — Fix: Reap exited stdio MCP server processes (zombie cleanup)
- [#8947](https://github.com/zeroclaw-labs/zeroclaw/pull/8947) — Fix: Honor provider timeout config for Anthropic (instead of hardcoded 120s)
- [#8954](https://github.com/zeroclaw-labs/zeroclaw/pull/8954) — Feature: Multi-arch Alpine/musl Docker image via cargo-zigbuild
- [#8949](https://github.com/zeroclaw-labs/zeroclaw/pull/8949) — Feature: Webhook GET + challenge-echo for plugin verification
- [#8923](https://github.com/zeroclaw-labs/zeroclaw/pull/8923) — Feature: Host-mediated outbound raw TCP (+TLS) for channel plugins (size:XL)
- [#8909](https://github.com/zeroclaw-labs/zeroclaw/pull/8909) — Feature: Gateway and dashboard capability catalog (size:XL)
- [#8908](https://github.com/zeroclaw-labs/zeroclaw/pull/8908) — Feature: Unified capability catalog + plugin enable/disable CLI (size:XL)
- [#8880](https://github.com/zeroclaw-labs/zeroclaw/pull/8880) — Feature: SOP approval broker with group membership and quorum (size:XL)

## Community Hot Topics

**Most discussed issues** (by comment count):

1. **[#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) — [Bug]: Agent appends subsequent image in each request on Telegram** (6 comments, open since April)  
   *User reports that sending two+ images on Telegram triggers duplicate agent responses. The fix touches gateway/runtime channel logic for Telegram image handling.*

2. **[#8654](https://github.com/zeroclaw-labs/zeroclaw/issues/8654) — [Bug]: skill-review fork panics (SIGSEGV) after tool-heavy turn** (3 comments, open, risk:high)  
   *Agent crashes hard with a segmentation fault when the skill-review background fork hits an out-of-range slice access in `skills/review.rs:159`. Critical stability issue.*

3. **[#8798](https://github.com/zeroclaw-labs/zeroclaw/issues/8798) — RFC: Consolidate /ws/chat and /acp onto single wire protocol** (2 comments, open, risk:high)  
   *Design RFC proposing to merge two parallel WebSocket channels into one unified protocol, reducing 2132-line bespoke event stream complexity.*

4. **[#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) — Feature: Comfy Cloud as shared media provider** (2 comments, open, risk:high)  
   *User requests ComfyUI integration as a first-class media generation provider, including groundwork for a future `gen_video` tool.*

**Most active PRs** by size/interaction — the **plugins infrastructure stack** from JordanTheJet dominates: [#8923](https://github.com/zeroclaw-labs/zeroclaw/pull/8923) (TCP/TLS outbound), [#8909](https://github.com/zeroclaw-labs/zeroclaw/pull/8909) (capability catalog), [#8908](https://github.com/zeroclaw-labs/zeroclaw/pull/8908) (plugin CLI), and [#8949](https://github.com/zeroclaw-labs/zeroclaw/pull/8949) (webhook verification) — all size:XL or stacked, signaling a major architectural push toward plugin extensibility.

## Bugs & Stability

**New bugs reported today** (2026-07-10/11), ranked by severity:

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **S1 - workflow blocked** | [#8934](https://github.com/zeroclaw-labs/zeroclaw/issues/8934) | Gemini function calls fail because `thought_signature` is dropped from assistant history — later model requests error out | No fix PR yet |
| **S1 - workflow blocked** | [#8950](https://github.com/zeroclaw-labs/zeroclaw/issues/8950) | Telegram `setMyCommands` rejected with `BOT_COMMANDS_TOO_MUCH` when tools+skills+builtins exceed 100 — command menu never registers | No fix PR yet |
| **S2 - degraded behavior** | [#8936](https://github.com/zeroclaw-labs/zeroclaw/issues/8936) | `loop_detector::hash_value` deep-clones entire tool-args JSON tree on every tool call (hot path, RSS growth) | No fix PR yet |
| **S2 - degraded behavior** | [#8929](https://github.com/zeroclaw-labs/zeroclaw/issues/8929) | Streamed narration duplicated when final display text is trimmed | No fix PR |
| **S2 - degraded behavior** | [#8945](https://github.com/zeroclaw-labs/zeroclaw/issues/8945) | ZeroCode input box blocks macOS text replacements | No fix PR |
| **S2 - degraded behavior** | [#8944](https://github.com/zeroclaw-labs/zeroclaw/issues/8944) | ZeroCode transcript mouse copy blocks word-level text selection | No fix PR |
| **S2 - degraded behavior** | [#8952](https://github.com/zeroclaw-labs/zeroclaw/issues/8952) | Streamed pre-tool narration duplicated when turn text has whitespace | No fix PR |

**Existing high-risk bugs with active fix PRs:**
- [#8654](https://github.com/zeroclaw-labs/zeroclaw/issues/8654) — skill-review SIGSEGV (risk:high, no public fix PR yet)
- [#8810](https://github.com/zeroclaw-labs/zeroclaw/issues/8810) — Telegram documentation is wrong (risk:low, PR [#8825](https://github.com/zeroclaw-labs/zeroclaw/pull/8825) open)
- [#8938](https://github.com/zeroclaw-labs/zeroclaw/pull/8938) — CI fix: duplicated rustdoc flag breaks `cargo test --doc`

## Feature Requests & Roadmap Signals

**Key feature requests received today:**
- [#8958](https://github.com/zeroclaw-labs/zeroclaw/issues/8958) — **ACP agent selection via `?agent=` query param** (multi-agent endpoints for external clients). Requested by `metalmon` after validating with Thunderbolt (Mozilla Thunderbird's ACP client). *Likely in v0.8.4 — signals demand for multi-tenant gateway.*

- [#8933](https://github.com/zeroclaw-labs/zeroclaw/issues/8933) — **Add `gen_ai.conversation.id` for cross-turn session correlation in OTel export**. *Fits the v0.8.3 observability tracker [#8073](https://github.com/zeroclaw-labs/zeroclaw/issues/8073); likely to land soon.*

- [#8956](https://github.com/zeroclaw-labs/zeroclaw/issues/8956) — **Localize pre-existing `skills install` error paths through Fluent** (refactoring, not user-facing). *Part of ongoing i18n/localization push.*

**Roadmap signals from open RFCs:**
- [#8798](https://github.com/zeroclaw-labs/zeroclaw/issues/8798) — Consolidate `/ws/chat` and `/acp` onto single wire protocol. *This is a major architectural RFC; if accepted, it would simplify the 2132-line websocket handler and reduce maintenance burden.*

**Predictions for next version (v0.8.3+):**
- Plugin capability catalog + CLI tools (based on [#8908](https://github.com/zeroclaw-labs/zeroclaw/pull/8908), [#8909](https://github.com/zeroclaw-labs/zeroclaw/pull/8909))
- Outbound TCP/TLS for channel plugins (based on [#8923](https://github.com/zeroclaw-labs/zeroclaw/pull/8923))
- SOP approval broker with quorum (based on [#8880](https://github.com/zeroclaw-labs/zeroclaw/pull/8880))
- Webhook verification handshake support for plugins (based on [#8949](https://github.com/zeroclaw-labs/zeroclaw/pull/8949))

## User Feedback Summary

**Real user pain points expressed recently:**
- *"Slop remains slop"* — user `cr3a7ure` ([#8810](https://github.com/zeroclaw-labs/zeroclaw/issues/8810)) expressing frustration with incorrect Telegram documentation and wrong command output, implying the quality of documentation is undermining the value of Rust's safety guarantees.
- **Telegram bot command registration broken** when tool count exceeds 100 ([#8950](https://github.com/zeroclaw-labs/zeroclaw/issues/8950)) — blocks users with many configured tools/skills from using Telegram slash commands at all.
- **macOS text replacements blocked** in ZeroCode TUI ([#8945](https://github.com/zeroclaw-labs/zeroclaw/issues/8945)) — impacts macOS users' muscle memory and productivity.
- **Gemini function calls completely blocked** ([#8934](https://github.com/zeroclaw-labs/zeroclaw/issues/8934)) — S1 severity, making Gemini unusable for tool-calling workflows.
- **MCP server zombie processes** ([#8948](https://github.com/zeroclaw-labs/zeroclaw/pull/8948)) — users running long-lived daemons would see accumulating defunct processes.

**Satisfaction signals:**
- External validation: ACP server tested successfully against Thunderbolt client ([#8958](https://github.com/zeroclaw-labs/zeroclaw/issues/8958)) — interoperability success.
- Multi-arch container work ([#8954](https://github.com/zeroclaw-labs/zeroclaw/pull/8954)) suggests real deployment demand on Apple Silicon and Proxmox environments.

## Backlog Watch

**Issues needing maintainer attention:**
- [#5514](https://github.com/zeroclaw-labs/zeroclaw/issues/5514) — **Open since April 8** (3+ months). Telegram image duplication bug with `help wanted` and `no-stale` labels. Six comments, no fix PR. Needs maintainer triage or assignment.
- [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) — **Open since May 10** (2 months). Comfy Cloud media provider feature request with `risk:high` and `status:accepted` — accepted but no implementation started.
- [#8798](https://github.com/zeroclaw-labs/zeroclaw/issues/8798) — **Needs-maintainer-review** RFC on WebSocket consolidation. 2 comments, no maintainer response yet.

**Stale PRs of concern:**
- [#8638](https://github.com/zeroclaw-labs/zeroclaw/pull/8638) — Open since July 3 (8 days), size:L, replacing ClawHub with git-catalog. No merge activity. This is a **breaking change** (`!` in title) that may require careful review.
- [#8139](https://github.com/zeroclaw-labs/zeroclaw/pull/8139) — Open since June 22 (19 days). TTL-based session cleanup for channels. Size:M, risk:high. No recent maintainer activity.

**No action required:**
- [#8397](https://github.com/zeroclaw-labs/zeroclaw/issues/8397) and [#8677](https://github.com/zeroclaw-labs/zeroclaw/issues/8677) — both closed today, the `uses_memory` flag feature has been delivered across CLI and web UI.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*